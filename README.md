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
- 상세 견적 조회<br>
- 메인 페이지 팝업창<br>
- 마이페이지(내 정보 수정, 찜 목록(장바구니), 예약 확인(환불처리, 진행 상황))<br>
- 게시판(게시글 출력, 페이징 처리, session을 이용해 회원과 관리자의 기능 구분(글삭제, 댓글기능, 댓글삭제))<br>
- 회원가입<br>
## ModalBasic.jsx 컴포넌트

※ 1. 상세 견적 조회

```javascript

export default (props) => {
    const [ttslider, setTtslider]= useState({
        ws:true,
        ss:false,
        ps:false,
        hs:false
    })
    const [pboxp, setPboxp] = useState({wprice:0,sprice:0,pprice:0,hprice:0,total:0});
    const [wchecked, setWchecked] = useState();
    const [sdmchecked, setSdmchecked] = useState();
    const [pchecked, setPchecked] = useState();
    const [hchecked, setHchecked] = useState();
    const [conditionData, setConditionData] = useState({
        wdate : "0001-01-01",
        wseoul : "데이터없음",
        wgyeong : "데이터없음",
        win : "데이터없음",
        wgang : "데이터없음",
        wje : "데이터없음",
        wdae : "데이터없음",
        wchungbuk : "데이터없음",
        wchungnam : "데이터없음",
        wbu : "데이터없음",
        wul : "데이터없음",
        wgyeongnam : "데이터없음",
        wdaegu : "데이터없음",
        wgyeongbuk : "데이터없음",
        wgwang : "데이터없음",
        wminprice : 0,
        wmaxprice: 0,
        wjeonnam : "데이터없음",
        wjeonbuk : "데이터없음",
        whole : "데이터없음",
        common : "데이터없음",
        trad : "데이터없음",
        hotel : "데이터없음",
        house : "데이터없음",
        church : "데이터없음",
        cathedral : "데이터없음",
        outdoor : "데이터없음",
        sdate : "0001-01-01",
        sseoul : "데이터없음",
        sgyeong : "데이터없음",
        sin : "데이터없음",
        sgang : "데이터없음",
        sje : "데이터없음",
        sdae : "데이터없음",
        schungbuk : "데이터없음",
        schungnam : "데이터없음",
        sbu : "데이터없음",
        sul : "데이터없음",
        sgyeongnam : "데이터없음",
        sdaegu : "데이터없음",
        sgyeongbuk : "데이터없음",
        sgwang : "데이터없음",
        sjeonnam : "데이터없음",
        sjeonbuk : "데이터없음",
        sminprice : 0,
        smaxprice: 0,
        pdate : "0001-01-01",
        pminprice : 0,
        pmaxprice: 0,
        hdate : "0001-01-01",
        hseoul : "해외",
        hgyeong : "데이터없음",
        hin : "데이터없음",
        hgang : "데이터없음",
        hje : "데이터없음",
        hdae : "데이터없음",
        hchungbuk : "데이터없음",
        hchungnam : "데이터없음",
        hbu : "데이터없음",
        hul : "데이터없음",
        hgyeongnam : "데이터없음",
        hdaegu : "데이터없음",
        hgyeongbuk : "데이터없음",
        hgwang : "데이터없음",
        hjeonnam : "데이터없음",
        hjeonbuk : "데이터없음",
        hminprice : 0,
        hmaxprice: 0  
    }
    );
    const [searchEstData, setSearchEstData] = useState(
        [{
            whidx :0,
            whprice : 0,
            whstr: "",
            whkind: "",
            whwcidx: "",
        }],
        [{
            sidx :0,
            scomp :"",
            sphone : "",
            sprice : 0,
            slocation : "",
            sstr: "",
            scomp: "",
        }],
        [{
            pidx :0,
            pphone : "",
            pprice : 0,
            pstr : '',
        }],
        [{
            hidx :0,
            hphone : "",
            hcost : 0,
            hstr: "",
            hlocation: "",
            hbramd: "",
        }]
    );
    
    
    const TRslider = () => {
        if(ttslider.ws===true){
            setTtslider({
                ...ttslider,
                ws:false,
                ss:true,
                ps:false,
                hs:false
            })
        }else if(ttslider.ss===true){
            setTtslider({
                ...ttslider,
                ws:false,
                ss:false,
                ps:true,
                hs:false,
            })
        }else if(ttslider.ps===true){
            setTtslider({
                ...ttslider,
                ws:false,
                ss:false,
                ps:false,
                hs:true,
            })
        }
    }
    const TLslider = () => {
        if(ttslider.hs===true){
            setTtslider({
                ...ttslider,
                ws:false,
                ss:false,
                ps:true,
                hs:false
            })
        }else if(ttslider.ps===true){
            setTtslider({
                ...ttslider,
                ws:false,
                ss:true,
                ps:false,
                hs:false,
            })
        }else if(ttslider.ss===true){
            setTtslider({
                ...ttslider,
                ws:true,
                ss:false,
                ps:false,
                hs:false,
            })
        }
    }

    
    const ClickLabel = (e) => {
        if(e.target.checked==false){
            setConditionData({
                ...conditionData,
                [e.target.name]: "데이터없음",
            })
        }else if(e.target.checked==true){
            setConditionData({
                ...conditionData,
                [e.target.name] : e.target.value
            })
        }
        console.log(e.target);
        console.log(conditionData);
        console.log(e.target.checked);
    }
    const ClickDate = (e) => {
        setConditionData({
            ...conditionData,
            [e.target.name] : e.target.value
        })

        const pnoRegExp = /^[0-9]{0,5}$/;


        if(!pnoRegExp.test(conditionData.hminprice)||!pnoRegExp.test(conditionData.hmaxprice)||!pnoRegExp.test(conditionData.sminprice)||!pnoRegExp.test(conditionData.smaxprice)||!pnoRegExp.test(conditionData.pminprice)||!pnoRegExp.test(conditionData.pmaxprice)||!pnoRegExp.test(conditionData.wminprice)||!pnoRegExp.test(conditionData.wmaxprice)){
            alert("5자리이내의 숫자만 입력해주세요.");
            e.target.value="";
        }
        console.log(e.target);
        console.log(conditionData);
    }

    const labelColor = (e) => {
        if(e.target.style.color=="black"){
            e.target.style.color="lightGray";
        }else {
            e.target.style.color="black"
        }
    }

    const postEst = () => {
        setPboxp({...pboxp,
            wprice:0,
            sprice:0,
            pprice:0,
            hprice:0,});
        console.log("ㅋㅋ"+pboxp);
        axios.post("/searchEstimate",JSON.stringify(conditionData),{params : conditionData})
        .then((response) => {
            console.log(response.data.p);
            console.log(response.data);
            setSearchEstData(response.data);
            console.log(searchEstData);
        })
        .catch((error) => {
            console.log(error);
        })
        console.log(searchEstData);
    }
    
    const rankingData0 =[
        { name: <span style={{fontSize:20, display:"flex", justifyContent:"space-around"}}>
        <div><input type="checkbox" style={{width:"20px", zoom: 2,verticalAlign:"-3px", display:"none"}} id="wchecked"  onClick={(e)=>{setTtslider({...ttslider, ws:true, ss:false, ps:false, hs:false});e.target.style.color="hotPink"}} value={1} checked/>{ttslider.ws ? <label id="wlabel" htmlFor='wchecked' style={{color:"hotPink", fontWeight:"bold"}}>웨딩홀</label>:<label id="wlabel" htmlFor='wchecked'>웨딩홀</label>}</div>
        <div><input type="checkbox" style={{width:"20px", zoom: 2,verticalAlign:"-3px", display:"none"}} id="sdmchecked" onClick={(e)=>{setTtslider({...ttslider, ws:false, ss:true, ps:false, hs:false});e.target.style.color="hotPink"}} value={1}/>{ttslider.ss ? <label id="slabel" htmlFor='sdmchecked' style={{color:"hotPink", fontWeight:"bold"}}>스드메</label>:<label id="slabel" htmlFor='sdmchecked'>스드메</label>}</div>
        <div><input type="checkbox" style={{width:"20px", zoom: 2,verticalAlign:"-3px", display:"none"}} id="pchecked" onClick={(e)=>{setTtslider({...ttslider, ws:false, ss:false, ps:true, hs:false});e.target.style.color="hotPink"}} value={1}/>{ttslider.ps ? <label id="plabel" htmlFor='pchecked' style={{color:"hotPink", fontWeight:"bold"}}>플래너</label>:<label id="plabel" htmlFor='pchecked'>플래너</label>}</div>
        <div><input type="checkbox" style={{width:"20px", zoom: 2,verticalAlign:"-3px", display:"none"}} id="hchecked" onClick={(e)=>{setTtslider({...ttslider, ws:false, ss:false, ps:false, hs:true});e.target.style.color="hotPink"}} value={1}/>{ttslider.hs ? <label id="hlabel" htmlFor='hchecked' style={{color:"hotPink", fontWeight:"bold"}}>허니문</label>:<label id="hlabel" htmlFor='hchecked'>허니문</label>}</div></span>,
        type: <div style={{textAlign:"left", fontSize:20, width:"100%", borderRight:"1px solid #0000000a"}}></div>
        },
    ]
    const rankingData1 = [
        { name: <span style={{fontSize:20}}>
            <span style={{display:"flex", justifyContent:"space-around"}}>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wseoul" name="wseoul" onChange={(e)=>{ ClickLabel(e)}}value={"서울"}  /><label onClick={(e) => labelColor(e)} htmlFor='wseoul' >서울</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wgyeong" name="wgyeong" onChange={(e)=>{ ClickLabel(e)}} value={"경기"}  /><label onClick={(e) => labelColor(e)} htmlFor='wgyeong'>경기</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="win" name="win" onChange={(e)=>{ ClickLabel(e)}} value={"인천"}  /><label onClick={(e) => labelColor(e)} htmlFor='win'>인천</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wgang" name="wgang" onChange={(e)=>{ ClickLabel(e)}} value={"강원"}  /><label onClick={(e) => labelColor(e)} htmlFor='wgang'>강원</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wje"onChange={(e)=>{ ClickLabel(e)}} name="wje" value={"제주"}  /><label onClick={(e) => labelColor(e)} htmlFor='wje'>제주</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wdae"onChange={(e)=>{ ClickLabel(e)}} name="wdae" value={"대전"}  /><label onClick={(e) => labelColor(e)} htmlFor='wdae'>대전</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wchungbuk"onChange={(e)=>{ ClickLabel(e)}} name="wchungbuk" value={"충북"}  /><label onClick={(e) => labelColor(e)} htmlFor='wchungbuk'>충북</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wchungnam"onChange={(e)=>{ ClickLabel(e)}} name="wchungnam" value={"충남"}  /><label onClick={(e) => labelColor(e)} htmlFor='wchungnam'>충남</label></div>
            </span>
            <br/>
            <span style={{display:"flex", justifyContent:"space-around"}}>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wbu" onChange={(e)=>{ ClickLabel(e)}} name="wbu" value={"스위스"} /><label onClick={(e)=>labelColor(e)} htmlFor='wbu'>부산</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wul" onChange={(e)=>{ ClickLabel(e)}} name="wul" value={"체코"} /><label onClick={(e)=>labelColor(e)} htmlFor='wul'>울산</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wgyeongnam" onChange={(e)=>{ ClickLabel(e)}} name="wgyeongnam" value={"경남"} /><label onClick={(e)=>labelColor(e)} htmlFor='wgyeongnam'>경남</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wdaegu" onChange={(e)=>{ ClickLabel(e)}} name="wdaegu" value={"포르투갈"} /><label onClick={(e)=>labelColor(e)} htmlFor='wdaegu'>대구</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wgyeongbuk" onChange={(e)=>{ ClickLabel(e)}} name="wgyeongbuk" value={"경북"} /><label onClick={(e)=>labelColor(e)} htmlFor='wgyeongbuk'>경북</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wgwang" onChange={(e)=>{ ClickLabel(e)}} name="wgwang" value={"광주"} /><label onClick={(e)=>labelColor(e)} htmlFor='wgwang'>광주</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wjeonnam" onChange={(e)=>{ ClickLabel(e)}} name="wjeonnam" value={"전남"} /><label onClick={(e)=>labelColor(e)} htmlFor='wjeonnam'>전남</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="wjeonbuk" onChange={(e)=>{ ClickLabel(e)}} name="wjeonbuk" value={"전북"} /><label onClick={(e)=>labelColor(e)} htmlFor='wjeonbuk'>전북</label></div>
            </span>
            </span>,
            type: <div style={{textAlign:"left", fontSize:20, width:"100%", height:"80px", lineHeight:"40px", borderRight:"1px solid #0000000a"}}>웨딩홀 &nbsp;위치</div>
        },
        { name: 
            <InputGroup><input type={"date"}style={{ marginLeft:-50, fontSize:"18px", border:"none", padding:"8px" ,textAlign:"center"}} name="wdate" onChange={(e)=>ClickDate(e)}></input></InputGroup>,
            type: <div style={{textAlign:"left", fontSize:20, width:"100%", lineHeight:"40px",borderRight:"1px solid #0000000a"}}>웨딩홀 &nbsp;날짜</div>
        },
        { name: <span style={{fontSize:20}}>
            <span style={{display:"flex", justifyContent:"space-around"}}>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="whole" name="whole" onChange={(e)=>{ ClickLabel(e)}}value={"전체"}  /><label onClick={(e) => labelColor(e)} htmlFor='whole' >전체</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="common" name="common" onChange={(e)=>{ ClickLabel(e)}} value={"일반"}  /><label onClick={(e) => labelColor(e)} htmlFor='common'>일반</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="trad" name="trad" onChange={(e)=>{ ClickLabel(e)}} value={"전통혼례"}  /><label onClick={(e) => labelColor(e)} htmlFor='trad'>전통혼례</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hotel"onChange={(e)=>{ ClickLabel(e)}} name="hotel" value={"호텔"}  /><label onClick={(e) => labelColor(e)} htmlFor='hotel'>호텔</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="house"onChange={(e)=>{ ClickLabel(e)}} name="house" value={"하우스"}  /><label onClick={(e) => labelColor(e)} htmlFor='house'>하우스</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="church"onChange={(e)=>{ ClickLabel(e)}} name="church" value={"교회"}  /><label onClick={(e) => labelColor(e)} htmlFor='church'>교회</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="cathedral"onChange={(e)=>{ ClickLabel(e)}} name="cathedral" value={"성당"}  /><label onClick={(e) => labelColor(e)} htmlFor='cathedral'>성당</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="outdoor" name="outdoor" onChange={(e)=>{ ClickLabel(e)}} value={"야외"}  /><label onClick={(e) => labelColor(e)} htmlFor='outdoor'>야외</label></div>
            </span>
            </span>,
            type: <div style={{textAlign:"left", fontSize:20, width:"100%", height:"80px", lineHeight:"40px", borderRight:"1px solid #0000000a"}}>웨딩홀 &nbsp;타입</div>
        },
        {   name:<div style={{display:"flex", marginLeft:"50px", alignItems:"center"}}>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px", marginLeft:"100px"}} name="wminprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{ margin:"0 20px",width:"50px", marginLeft:"1%"}}>만원</h3><h3 style={{marginRight:"2%"}}> ~ </h3>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px"}} name="wmaxprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{marginLeft:"-1%",width:"100px"}}>만원</h3><Button onClick={() => {postEst()}} style={{ width:"100px",height:"70px", marginLeft:120,background:'#c9a3b6', borderRadius:'10px'}}>검색</Button>
            </div>,
            type: <div style={{textAlign:"left", fontSize:20, width:"100%", borderRight:"1px solid #0000000a"}}>웨딩홀 &nbsp;가격</div>},
        ]
    const rankingData2 =[
        { name: 
            <InputGroup><input type={"date"}style={{ marginLeft:-50, textAlign:"center", fontSize:"18px", border:"none", padding:"8px"}} name="sdate" onChange={(e)=>ClickDate(e)}></input></InputGroup>,
            type: <div style={{textAlign:"left", fontSize:20, width:"100%", lineHeight:"40px",borderRight:"1px solid #0000000a"}}>스드메 &nbsp;날짜</div>
        },
        { name: <span style={{fontSize:20}}>
            <span style={{display:"flex", justifyContent:"space-around"}}>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sseoul"onChange={(e)=>{ ClickLabel(e)}} name="sseoul" value={"서울"}  /><label onClick={(e)=>labelColor(e)} htmlFor='sseoul'>서울</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sgyeong"onChange={(e)=>{ ClickLabel(e)}} name="sgyeong" value={"경기"}  /><label onClick={(e)=>labelColor(e)} htmlFor='sgyeong'>경기</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sin"onChange={(e)=>{ ClickLabel(e)}} name="sin" value={"인천"}  /><label onClick={(e)=>labelColor(e)} htmlFor='sin'>인천</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sgang"onChange={(e)=>{ ClickLabel(e)}} name="sgang" value={"강원"}  /><label onClick={(e)=>labelColor(e)} htmlFor='sgang'>강원</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sje"onChange={(e)=>{ ClickLabel(e)}} name="sje" value={"제주"}  /><label onClick={(e)=>labelColor(e)} htmlFor='sje'>제주</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sdae"onChange={(e)=>{ ClickLabel(e)}} name="sdae" value={"대전"}  /><label onClick={(e)=>labelColor(e)} htmlFor='sdae'>대전</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="schungbuk"onChange={(e)=>{ ClickLabel(e)}} name="schungbuk" value={"충북"}  /><label onClick={(e)=>labelColor(e)} htmlFor='schungbuk'>충북</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="schungnam"onChange={(e)=>{ ClickLabel(e)}} name="schungnam" value={"충남"}  /><label onClick={(e)=>labelColor(e)} htmlFor='schungnam'>충남</label></div>
            </span>
            <br/>
            <span style={{display:"flex", justifyContent:"space-around"}}>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sbu" onChange={(e)=>{ ClickLabel(e)}} name="sbu" value={"부산"} /><label onClick={(e)=>labelColor(e)} htmlFor='sbu'>부산</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sul" onChange={(e)=>{ ClickLabel(e)}} name="sul" value={"울산"} /><label onClick={(e)=>labelColor(e)} htmlFor='sul'>울산</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sgyeongnam" onChange={(e)=>{ ClickLabel(e)}} name="sgyeongnam" value={"경남"} /><label onClick={(e)=>labelColor(e)} htmlFor='sgyeongnam'>경남</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sdaegu" onChange={(e)=>{ ClickLabel(e)}} name="sdaegu" value={"대구"} /><label onClick={(e)=>labelColor(e)} htmlFor='sdaegu'>대구</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sgyeongbuk" onChange={(e)=>{ ClickLabel(e)}} name="sgyeongbuk" value={"경북"} /><label onClick={(e)=>labelColor(e)} htmlFor='sgyeongbuk'>경북</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sgwang" onChange={(e)=>{ ClickLabel(e)}} name="sgwang" value={"광주"} /><label onClick={(e)=>labelColor(e)} htmlFor='sgwang'>광주</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sjeonnam" onChange={(e)=>{ ClickLabel(e)}} name="sjeonnam" value={"전남"} /><label onClick={(e)=>labelColor(e)} htmlFor='sjeonnam'>전남</label></div>
                <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="sjeonbuk" onChange={(e)=>{ ClickLabel(e)}} name="sjeonbuk" value={"전북"} /><label onClick={(e)=>labelColor(e)} htmlFor='sjeonbuk'>전북</label></div>
            </span>
            </span>,
            type: <div style={{textAlign:"left", fontSize:20, width:"100%", height:"80px", lineHeight:"40px", borderRight:"1px solid #0000000a"}}>스드메 &nbsp;위치</div>
        },
        { name:<div style={{display:"flex", marginLeft:"50px", alignItems:"center"}}>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px", marginLeft:"100px"}} name="sminprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{ margin:"0 20px",width:"50px", marginLeft:"1%"}}>만원</h3><h3 style={{marginRight:"2%"}}> ~ </h3>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px"}} name="smaxprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{marginLeft:"-1%",width:"100px"}}>만원</h3><Button onClick={() => {postEst()}} style={{ width:"100px",height:"70px", marginLeft:120, background:'#c9a3b6', borderRadius:'10px'}}>검색</Button>
            </div>,
            type: <div style={{textAlign:"left", fontSize:20, width:"100%", borderRight:"1px solid #0000000a"}}>스드메 &nbsp;가격</div>
    },]
    const rankingData3 = [
        { name: 
            <InputGroup><input type={"date"}style={{ marginLeft:-50, textAlign:"center", fontSize:"18px", border:"none", padding:"8px"}} name="pdate" onChange={(e)=>ClickDate(e)}></input></InputGroup>,
        type: <div style={{textAlign:"left", fontSize:20, width:"100%", lineHeight:"40px",borderRight:"1px solid #0000000a"}}>플래너 &nbsp;날짜</div>
        },
        { name:<div style={{display:"flex", marginLeft:"50px", alignItems:"center"}}>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px", marginLeft:"100px"}} name="pminprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{ margin:"0 20px",width:"50px", marginLeft:"1%"}}>만원</h3><h3 style={{marginRight:"2%"}}> ~ </h3>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px"}} name="pmaxprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{marginLeft:"-1%",width:"100px"}}>만원</h3><Button onClick={() => {postEst()}} style={{ width:"100px",height:"70px", marginLeft:120,background:'#c9a3b6', borderRadius:'10px'}}>검색</Button>
            </div>,
        type: <div style={{textAlign:"left", fontSize:20, width:"100%", borderRight:"1px solid #0000000a"}}>플래너 &nbsp;가격</div>
    },]
    const rankingData4 = [
    { name: 
        <InputGroup><input type={"date"}style={{ marginLeft:-50, textAlign:"center", fontSize:"18px", border:"none", padding:"8px"}} name="hdate" onChange={(e)=>ClickDate(e)}></input></InputGroup>,
        type: <div style={{textAlign:"left", fontSize:20, width:"100%",lineHeight:"40px" ,borderRight:"1px solid #0000000a"}}>허니문 &nbsp;날짜</div>
    },
    { name: <span style={{fontSize:20}}>
        <span style={{display:"flex", justifyContent:"space-around"}}>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hseoul"onChange={(e)=>{ ClickLabel(e)}} name="hseoul" value={"국내"} /><label onClick={(e)=>labelColor(e)} htmlFor='hseoul'>국내</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hgyeong"onChange={(e)=>{ ClickLabel(e)}} name="hgyeong" value={"태국"} /><label onClick={(e)=>labelColor(e)} htmlFor='hgyeong'>태국</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hin"onChange={(e)=>{ ClickLabel(e)}} name="hin" value={"발리"} /><label onClick={(e)=>labelColor(e)} htmlFor='hin'>발리</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hgang"onChange={(e)=>{ ClickLabel(e)}} name="hgang" value={"하와이"} /><label onClick={(e)=>labelColor(e)} htmlFor='hgang'>하와이</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hje"onChange={(e)=>{ ClickLabel(e)}} name="hje" value={"몰디브"} /><label onClick={(e)=>labelColor(e)} htmlFor='hje'>몰디브</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hdae"onChange={(e)=>{ ClickLabel(e)}} name="hdae" value={"칸쿤"} /><label onClick={(e)=>labelColor(e)} htmlFor='hdae'>칸쿤</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hchungbuk"onChange={(e)=>{ ClickLabel(e)}} name="hchungbuk" value={"파리"} /><label onClick={(e)=>labelColor(e)} htmlFor='hchungbuk'>파리</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hchungnam"onChange={(e)=>{ ClickLabel(e)}} name="hchungnam" value={"이태리"} /><label onClick={(e)=>labelColor(e)} htmlFor='hchungnam'>이태리</label></div>
        </span>
        <br/>
        <span style={{display:"flex", justifyContent:"space-around"}}>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hbu" onChange={(e)=>{ ClickLabel(e)}} name="hbu" value={"스위스"} /><label onClick={(e)=>labelColor(e)} htmlFor='hbu'>스위스</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hul" onChange={(e)=>{ ClickLabel(e)}} name="hul" value={"체코"} /><label onClick={(e)=>labelColor(e)} htmlFor='hul'>체코</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hgyeongnam"el onChange={(e)=>{ ClickLabel(e)}} name="hgyeongnam" value={"포르투갈"} /><label onClick={(e)=>labelColor(e)} htmlFor='hgyeongnam'>포르투갈</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hdaegu" onChange={(e)=>{ ClickLabel(e)}} name="hdaegu" value={"스페인"} /><label onClick={(e)=>labelColor(e)} htmlFor='hdaegu'>스페인</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hgyeongbuk" onChange={(e)=>{ ClickLabel(e)}} name="hgyeongbuk" value={"모리셔스"} /><label onClick={(e)=>labelColor(e)} htmlFor='hgyeongbuk'>모리셔스</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hgwang" onChange={(e)=>{ ClickLabel(e)}} name="hgwang" value={"괌"} /><label onClick={(e)=>labelColor(e)} htmlFor='hgwang'>괌</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hjeonnam" onChange={(e)=>{ ClickLabel(e)}} name="hjeonnam" value={"사이판"} /><label onClick={(e)=>labelColor(e)} htmlFor='hjeonnam'>사이판</label></div>
            <div><input type="checkbox" style={{width:"20px", zoom: 2, verticalAlign:"-3px", display:"none"}} id="hjeonbuk" onChange={(e)=>{ ClickLabel(e)}} name="hjeonbuk" value={"두바이"} /><label onClick={(e)=>labelColor(e)} htmlFor='hjeonbuk'>두바이</label></div>
        </span>
        </span>,
        type: <div style={{textAlign:"left", fontSize:20, width:"100%", height:"80px", lineHeight:"40px", borderRight:"1px solid #0000000a"}}>허니문 &nbsp;위치</div>
        },
        { name:<div style={{display:"flex", marginLeft:"50px", alignItems:"center"}}>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px", marginLeft:"100px"}} name="hminprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{ margin:"0 20px",width:"50px", marginLeft:"1%"}}>만원</h3><h3 style={{marginRight:"2%"}}> ~ </h3>
            <input type={"text"} style={{width:"30%", fontSize:"18px", border:"1px solid #ddd", padding:"8px"}} name="hmaxprice" maxLength={5} onChange={(e)=>ClickDate(e)}></input><h3 style={{marginLeft:"-1%",width:"100px"}}>만원</h3><Button onClick={() => {postEst()}} style={{ width:"100px",height:"70px", marginLeft:120,background:'#c9a3b6', borderRadius:'10px'}}>검색</Button>
            </div>,
        type: <div style={{textAlign:"left", fontSize:20, width:"100%", borderRight:"1px solid #0000000a"}}>허니문 &nbsp;가격 </div>
        },
  ]

  const { w, s, p, h } = searchEstData;


  return (
    <>
    <Section title="상세견적" style={props.style} titleSize={"xl"}>
        <div className='slbtn' onClick={TLslider} style={{fontSize:"50px", position:"absolute", left:"80px", top:"85%"}}>«</div>
        <div className='slbtn' onClick={TRslider} style={{fontSize:"50px", position:"absolute", right:"80px", top:"85%"}}>»</div>
        <ETable
            style={{ marginTop: 30, marginBottom: "-30px", minWidth:"100%", zIndex:"10"}}
            data-aos="fade-up"
            columns={[ //배열
            {//예시
                name: '타입',
                id: 'type',
            },
            {//예시
                name: '이름',
                id: 'name',
            },
            ]}
            dataSource={rankingData0}
        />
            { ttslider.ws ? <div id='tcontainer' style={{minWidth:"100%", height:"450px" , overflow:"hidden", position:"relative", boxSizing:"border-box"}}>
        <ETable id="t1"
            style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:0, transition:"left 1s"}}
            data-aos="fade-up"
            columns={[ //배열
            {//예시
                name: '타입',
                id: 'type',
            },
            {//예시
                name: '이름',
                id: 'name',
            },
            ]}
            dataSource={rankingData1}
        />
                <ETable id="t2"
            style={{ marginTop: 30, minWidth:"100%", position:"absolute" , left:1500, transition:"left 1s"}}
            data-aos="fade-up"
            columns={[ //배열
            {//예시
                name: '타입',
                id: 'type',
            },
            {//예시
                name: '이름',
                id: 'name',
            },
            ]}
            dataSource={rankingData2}
        />
                <ETable id="t3"
            style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:3000, transition:"left 1s"}}
            data-aos="fade-up"
            columns={[ //배열
            {//예시
                name: '타입',
                id: 'type',
            },
            {//예시
                name: '이름',
                id: 'name',
            },
            ]}
            dataSource={rankingData3}
        />
                <ETable id="t4"
            style={{ marginTop: 30, minWidth:"100%", position:"absolute" , left:4500, transition:"left 1s"}}
            data-aos="fade-up"
            columns={[ //배열
            {//예시
                name: '타입',
                id: 'type',
            },
            {//예시
                name: '이름',
                id: 'name',
            },
            ]}
            dataSource={rankingData4}
        /></div>
: ttslider.ss ? <div id='tcontainer' style={{minWidth:"100%", height:"450px" , overflow:"hidden", position:"relative", boxSizing:"border-box"}}>
<ETable id="t1"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:-1500, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData1}
/>
        <ETable id="t2"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:0, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData2}
/>
        <ETable id="t3"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:1500, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData3}
/>
        <ETable id="t4"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:3000, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData4}
/></div>
: ttslider.ps ? <div id='tcontainer' style={{minWidth:"100%", height:"450px" , overflow:"hidden", position:"relative", boxSizing:"border-box"}}>
<ETable id="t1"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:-3000, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData1}
/>
        <ETable id="t2"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:-1500, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData2}
/>
        <ETable id="t3"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:0, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData3}
/>
        <ETable id="t4"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute" , left:1500, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData4}
/></div> 
: ttslider.hs ? <div id='tcontainer' style={{minWidth:"100%", height:"450px" , overflow:"hidden", position:"relative", boxSizing:"border-box"}}>
<ETable id="t1"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:-4500, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData1}
/>
        <ETable id="t2"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:-3000, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData2}
/>
        <ETable id="t3"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute", left:-1500, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData3}
/>
        <ETable id="t4"
    style={{ marginTop: 30, minWidth:"100%", position:"absolute" , left:0, transition:"left 1s"}}
    data-aos="fade-up"
    columns={[ //배열
    {//예시
        name: '타입',
        id: 'type',
    },
    {//예시
        name: '이름',
        id: 'name',
    },
    ]}
    dataSource={rankingData4}
/></div> : null}
    </Section>
    <EstimateResult eData={searchEstData} setPboxp={setPboxp} pboxp={pboxp}></EstimateResult>
    </>
  )
}
```
- #### 검색 테이블<br>
각 검색 조건의 input창에 onChange함수를 이용해 useState에 보관 후 '검색' 버튼 클릭시 axios를 사용해 JSON형태로 지정한 url로 보낸 후 intellij에서 받아 온 data들을 정렬해서 보여줍니다.<br>

## Back_EstimateController
```java
    @PostMapping("/searchEstimate")
    public Map SearchEstimate(String wdate, String wseoul, String wgyeong, String win, String wgang, String wje, String wdae, String wchungbuk, String wchungnam, String wbu, String wul, String wgyeongnam, String wdaegu, String wgyeongbuk, String wgwang, String wjeonnam, String wjeonbuk, String whole, String common, String trad, String hotel, String house, String church, String cathedral, String outdoor ,int wminprice, int wmaxprice, String sdate, String sseoul, String sgyeong, String sin, String sgang, String sje, String sdae, String schungbuk, String schungnam, String sbu, String sul, String sgyeongnam, String sdaegu, String sgyeongbuk, String sgwang, String sjeonnam, String sjeonbuk, int sminprice, int smaxprice, String pdate, int pminprice, int pmaxprice, String hdate, String hseoul, String hgyeong, String hin, String hgang, String hje, String hdae, String hchungbuk, String hchungnam, String hbu, String hul, String hgyeongnam, String hdaegu, String hgyeongbuk, String hgwang, String hjeonnam, String hjeonbuk, int hminprice, int hmaxprice){
        log.info("searchEstimate()");
//        log.info(wdate);
//        log.info(wseoul);
//        log.info(wgyeong);
//        log.info(win);
        Map last = eServ.searchEst(wdate, wseoul, wgyeong, win, wgang, wje, wdae, wchungbuk, wchungnam, wbu, wul, wgyeongnam, wdaegu, wgyeongbuk, wgwang, wjeonnam, wjeonbuk, whole, common, trad, hotel, house, church, cathedral, outdoor, wminprice, wmaxprice, sdate, sseoul, sgyeong, sin, sgang, sje, sdae, schungbuk, schungnam, sbu, sul, sgyeongnam, sdaegu, sgyeongbuk, sgwang, sjeonnam, sjeonbuk, sminprice, smaxprice, pdate, pminprice, pmaxprice, hdate, hseoul, hgyeong, hin, hgang, hje, hdae, hchungbuk, hchungnam, hbu, hul, hgyeongnam, hdaegu, hgyeongbuk, hgwang, hjeonnam, hjeonbuk, hminprice, hmaxprice);
        return last;
    }
    //searchEstimate end
```
## Back_EstimateService
```java
@Service
@Log
public class EstimateService {
    @Autowired
    private WeddingCompRepository wcRepo;
    @Autowired
    private WeddingHoleRepository whRepo;
    @Autowired
    private SDMRepository sRepo;
    @Autowired
    private PlannerRepository pRepo;
    @Autowired
    private HoneyMoonRepository hRepo;
    @Autowired
    private ReservationRepository rRepo;


    public Map searchEst(String wdate, String wseoul, String wgyeong, String win, String wgang, String wje, String wdae, String wchungbuk, String wchungnam, String wgyeongnam, String wdaegu, String wbu, String wul, String wgyeongbuk, String wgwang, String wjeonnam, String wjeonbuk, String whole, String common, String trad, String hotel, String house, String church, String cathedral, String outdoor, int wminprice, int wmaxprice, String sdate, String sseoul, String sgyeong, String sin, String sgang, String sje, String sdae, String schungbuk, String schungnam, String sbu, String sul, String sgyeongnam, String sdaegu, String sgyeongbuk, String sgwang, String sjeonnam, String sjeonbuk,  int sminprice, int smaxprice, String pdate, int pminprice, int pmaxprice, String hdate, String hseoul, String hgyeong, String hin, String hgang, String hje, String hdae, String hchungbuk, String hchungnam, String hbu, String hul, String hgyeongnam, String hdaegu, String hgyeongbuk, String hgwang, String hjeonnam, String hjeonbuk, int hminprice, int hmaxprice){
        List<WeddingComp> wcList;
        List<WeddingHall> whList = new ArrayList<>();
        List<Reservations> rwhList;
        List<WeddingHall> removewh = new ArrayList<>();
        List<SDM> sList;
        List<Reservations> rsList;
        List<SDM> removes = new ArrayList<>();
        List<Planner> pList;
        List<Reservations> rpList;
        List<Planner> removep = new ArrayList<>();
        List<HoneyMoon> hList;
        List<Reservations> rhList;
        List<HoneyMoon> removeh = new ArrayList<>();

        Map estData = new HashMap<>();
        log.info("날짜어떻게넘어옴?"+hdate);
        java.sql.Date cvtwdate = java.sql.Date.valueOf(wdate);
        java.sql.Date cvtsdate = java.sql.Date.valueOf(sdate);
        java.sql.Date cvtpdate = java.sql.Date.valueOf(pdate);
        java.sql.Date cvthdate = java.sql.Date.valueOf(hdate);
//        java.sql.Timestamp cvthdate = java.sql.Timestamp.valueOf(hdate+" 00:00:00");
            wcList = wcRepo.findBySWClocation(wseoul, wgyeong, win, wgang, wje, wdae, wchungbuk, wchungnam, wbu, wul, wgyeongnam, wdaegu, wgyeongbuk, wgwang, wjeonnam, wjeonbuk);
            log.info("이거시 서치결과"+wcList);
            for(WeddingComp wno : wcList){
                switch(whole){
                    case "데이터없음" :
                        if(common.equals("데이터없음") && trad.equals("데이터없음") && hotel.equals("데이터없음") && house.equals("데이터없음") && church.equals("데이터없음") && cathedral.equals("데이터없음") && outdoor.equals("데이터없음")){
                            whList.addAll(whRepo.findByWhwcidx3(wno.getWidx(), wminprice, wmaxprice));
                        }
                        else if(whRepo.findByWhwcidx2(wno.getWidx(), wminprice, wmaxprice, common, trad, hotel, house, church, cathedral, outdoor)!=null) {
                            whList.addAll(whRepo.findByWhwcidx2(wno.getWidx(), wminprice, wmaxprice, common, trad, hotel, house, church, cathedral, outdoor));
                        }
                        break;
                    case "전체" :
                        if(whRepo.findByWhwcidx3(wno.getWidx(), wminprice, wmaxprice)!=null) {
                            whList.addAll(whRepo.findByWhwcidx3(wno.getWidx(), wminprice, wmaxprice));
                        }
                    break;
                }
            }
            log.info("웨딩회사"+wcList);
            log.info("웨딩홀"+whList);

            rwhList = rRepo.findByRwhdate(cvtwdate);
            int index1=0;
            for(WeddingHall whno : whList){
                for(Reservations rno : rwhList){
                    if(rno.getRsidx()==whno.getWhidx()){
                        removewh.add(whList.get(index1));
                    }   //if end
                }   //for end
                index1++;
            }// for end
            whList.remove(removewh);
            log.info("웨딩홀에서 지역으로 검색해온 데이터에서 예약있는 데이터 제외한 결과"+whList);



            sList = sRepo.findBySSlocation(sseoul, sgyeong, sin, sgang, sje, sdae, schungbuk, schungnam, sbu, sul, sgyeongnam, sdaegu, sgyeongbuk, sgwang, sjeonnam, sjeonbuk, sminprice, smaxprice);
            log.info("이거시 서치결과"+sList);
        log.info(sList+"스드메");
            rsList = rRepo.findByRsdate(cvtsdate);
            int index2=0;
            for(SDM sno : sList){
                for(Reservations rno : rsList){
                    if(rno.getRsidx()==sno.getSidx()){
                        removes.add(sList.get(index2));
                    }   //if end
                }   //for end
                index2++;
            }// for end
            sList.removeAll(removes);
            log.info("스드메에서 지역으로 검색해온 데이터에서 예약있는 데이터 제외한 결과"+sList);




            pList = pRepo.findByPrice(pminprice, pmaxprice);
            log.info("이거시 서치결과"+pList);
        log.info(pList+"플래너");
            rpList = rRepo.findByRpdate(cvtpdate);
            int index3=0;
            for(Planner pno : pList){
                for(Reservations rno : rpList){
                    if(rno.getRpidx()==pno.getPidx()){
                        removep.add(pList.get(index3));
                    }   //if end
                }   //for end
                index3++;
            }// for end
            pList.removeAll(removep);
            log.info("스드메에서 지역으로 검색해온 데이터에서 예약있는 데이터 제외한 결과"+pList);


            hList = hRepo.findBySHlocation(hgyeong, hin, hgang, hje, hdae, hchungbuk, hchungnam, hbu, hul, hgyeongnam, hdaegu, hgyeongbuk, hgwang, hjeonnam, hjeonbuk, hminprice, hmaxprice);
log.info(hList+"허니문");
log.info(hseoul+"이거왜안되지?");
            if(hseoul.equals("국내")){
                List<HoneyMoon> hList2 = new ArrayList<>();
                hList2 = hRepo.findAllByHarrival(hseoul);
                hList.addAll(hList2);
                log.info("여기서안되나?"+hList);
            }
            rhList = rRepo.findByRhdate(cvthdate);
//            log.info("이거시 서치결과"+hList);
//            log.info("컨버팅된 결과" + cvthdate);
                int index4=0;
//                int index2=0;
            for(HoneyMoon hno : hList){
//                log.info("sadads"+hno);
//                log.info(""+hno.getHidx());
//                log.info("예약날짜"+rhList);
                for(Reservations rno : rhList){
                    if(rno.getRhidx()==hno.getHidx()){
//                        log.info("빼기전"+hList);
//                        log.info("빼기전"+hno);
//                        hList.remove(index1);
                        removeh.add(hList.get(index4));
//                        log.info("삭제할 목록"+removeh);
//                        log.info("after remove"+hList);
//                        hList.removeIf(item -> item.getHidx()==rno.getRhidx());
                    }   //if end
//                    log.info("포문 반복확인"+hList);
                }   //for end
                index4++;
            }// for end
            hList.removeAll(removeh);
        // if end
        log.info("스드메에서 지역으로 검색해온 데이터에서 예약있는 데이터 제외한 결과"+sList);
        log.info("허니문에서 지역으로 검색해온 데이터에서 예약있는 데이터 제외한 결과"+hList);

//        int i=0;
//        for(WeddingHall wno : whList){
//            for(SDM sno : sList){
//                for(Planner pno : pList){
//                    for(HoneyMoon hno : hList){
//                        int tcost = wno.getWhprice()+ sno.getSprice()+ pno.getPprice()+hno.getHcost();
//                        if(wno.getWhprice()+ sno.getSprice()+ pno.getPprice()+hno.getHcost()>= minprice && wno.getWhprice()+ sno.getSprice()+ pno.getPprice()+hno.getHcost()<= maxprice){
//                            estData.put(i,whList);
//                            i++;
//                            estData.put(i,sList);
//                            i++;
//                            estData.put(i,pList);
//                            i++;
//                            estData.put(i,hList);
//
//                        }   //if end
//                    }   //for end
//                }   //for end
//            }   //for end
//        }   //for end
        estData.put("w", whList);
        estData.put("s", sList);
        estData.put("p", pList);
        estData.put("h", hList);
        log.info("최종 데이터"+estData);
        return estData;
    }

    public Map<String, Object> estimateMain(String type, String location, int mincost, int maxcost) {
        log.info("estimateMain()");
        List<HoneyMoon> hm = new ArrayList<>();
        List<Planner> pl = new ArrayList<>();
        List<WeddingHall> wh = new ArrayList<>();
        List<SDM> sdm = new ArrayList<>();
        List<WeddingComp> wc = new ArrayList<>();
        Map<String, Object> eMain = new HashMap<>();

        try{
            switch(type){
                case "허니문":
                    hm = hRepo.estMainHm(location, mincost, maxcost);
                    break;
                case "플래너":
                    pl = pRepo.estMainpl(mincost, maxcost);
                    break;
                case "웨딩홀":
                    wc = wcRepo.findByWlocation(location);
                    if(!wc.isEmpty())
                        for(WeddingComp c : wc)
                            wh.add(whRepo.estMainWh(c.getWidx(),mincost, maxcost));
                    break;
                case "스드메":
                    sdm = sRepo.estMainWh(location, mincost, maxcost);
                    break;
            }
            log.info("검색 성공");

            eMain.put("hm", hm);
            eMain.put("pl", pl);
            eMain.put("wh", wh);
            eMain.put("sdm", sdm);
        }catch (Exception e){
            e.printStackTrace();
            log.info("검색 실패");
        }
        return eMain;
    }
}
```

    {
    SDM findBySidx(int sidx);

    @Query("SELECT s FROM SDM s WHERE (s.slocation Like %?1% or s.slocation Like %?2% or s.slocation Like %?3% or s.slocation Like %?4% or s.slocation Like %?5% or s.slocation Like %?6% or s.slocation Like %?7% or s.slocation Like %?8% or s.slocation Like %?9% or s.slocation Like %?10% or s.slocation Like %?11% or s.slocation Like %?12% or s.slocation Like %?13% or s.slocation Like %?14% or s.slocation Like %?15% or s.slocation Like %?16%) And (s.sprice between ?17 and ?18)")
    List<SDM> findBySSlocation(String sseoul, String sgyeong, String sin, String sgang, String sje, String sdae, String schungbuk, String schungnam, String sbu, String sul, String sgyeongnam, String daegu, String sgyeongbuk, String sgwang, String sjeonnam, String sjeonbuk, int wminprice, int wmaxprice);

    List<SDM> findByScompContaining(String str);

    @Query("SELECT s FROM SDM s WHERE((s.slocation=?1)AND(s.sprice>=?2)AND(s.sprice<=?3))")
    List<SDM> estMainWh(String slocation, int mincost, int maxcost);

    List<SDM> findAllBySidx(int sidx);

    SDM findByScompAndSphoneAndSstr(String scomp, String sphone, Object o);

    @Query("SELECT s FROM SDM s WHERE s.sstr IS NOT NULL")
    Page<SDM> findBySstr(Pageable pb);

    Page<SDM> findBySstrIsNull(Pageable pb);
}


    {
    List<Reservations> findByRmid(String rmid);

    @Query("Select rwh from Reservations rwh where( rwh.rdate=?1 and rwh.rtype='웨딩홀' )")
    List<Reservations> findByRwhdate(Date wdate);
    @Query("Select rs from Reservations rs where( rs.rdate=?1 and rs.rtype='스드메' )")
    List<Reservations> findByRsdate(Date sdate);
    @Query("Select rp from Reservations rp where( rp.rdate=?1 and rp.rtype='플래너')")
    List<Reservations> findByRpdate(Date pdate);
    @Query("Select rh from Reservations rh where( rh.rdate=?1 and rh.rtype='허니문')")
    List<Reservations> findByRhdate(Date hdate);

    List<Reservations> findByRtypeContaining(String str);

    List<Reservations> findByRmidContaining(String str);

    Reservations findByRsidx(int sidx);

    Reservations findByRhidx(int hidx);

    Reservations findByRwhidx(int whidx);

    Reservations findByRpidx(int pidx);

    List<Reservations> findByRtype(String rtype);

    int countByRwhidx(int whidx);

    int countByRmid(String mid);
    @Modifying
    @Transactional
    void deleteByRidx(int ridx);
    Reservations findByRidx(int ridx);

    Page<Reservations> findByRidxGreaterThan(int i, Pageable pb);
}

프론트에서 받아온 값을 매개변수로 받고 repository에서 쿼리문을 사용해 만든 함수 findByRsdate, findBySSlocation 등으로 데이터베이스에 일치하는 데이터를 가져온 후 데이터들을 카테고리별로 list에 담고 각 리스트들을 map에 담아서 return 합니다.<br><br>

- #### 검색 전 화면<br><br>
<img width="1109" alt="견적조회 테이블" src="https://user-images.githubusercontent.com/117880554/224933103-1a73367e-606d-40a6-b43f-b770d99f5547.png">

## EstimateItem.jsx 컴포넌트 (부분)

※ 로그인 회원, 비회원에 따라 다른 구성 

```javascript
const EstimateItem = ( {pboxp,setPboxp,w,s,p,h, ...props} ) => {
  const comma = (num) =>[num].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
  const id = sessionStorage.getItem("mid");
  const nextId = useRef(0);
  const [a, setA]= useState(false);
  const [tbox, setTbox]= useState(0);
  const clickTbox =()=>{setTbox(1)};
  const clickTbox2 = () => {setTbox(0);}
  // && pboxp.wprice!=w[e.target.id.substr(1)].whprice
  const dibBtn= () => {
    // axios.post("/ddibInsert" , null, {params:{dibData:encodeURI(dibData)}})
    axios.post("/ddibInsert" ,dibData)
    .then((res)=>{
      window.alert("찜딱콩");
      setA(false);
      setDibData([]);
    }).catch(err=>{setA(false);setDibData([]);});
  }
  const clickwItem = (e) => {
    if(id===undefined || id===null || id===""){
      window.alert("로그인 후 이용 가능한 서비스입니다.");
      return;
    }
    
    if(e.target.type==="submit"){
      let btnconfirm= window.confirm("찜하시겠습니까?");
      console.log(btnconfirm);
      if(btnconfirm===false){
        return;
      }
      else if(btnconfirm===true){
        setDibData([...dibData,{id:nextId.current ,dtype:"웨딩홀", dmid:id, dwhidx:w[e.target.id.substr(1)]?.whidx}]);
      }
      console.log(dibData);
      console.log(pboxp);
      setA(true);
      return;
    }

    const wc = document.getElementById("w"+e.target.id.substr(1));
    console.log("쫌"+wc.checked);
    console.log(w[e.target.id.substr(1)]);
      if(wc.checked==false){
      e.target.style.opacity=0.1;
        setPboxp({...pboxp, wprice:pboxp.wprice+w[e.target.id.substr(1)].whprice});
        setDibData([...dibData,{id:nextId.current ,dtype:"웨딩홀", dmid:id, dwhidx:w[e.target.id.substr(1)].whidx}]);
        console.log(dibData);
      }else{
        e.target.style.opacity=0;
        setPboxp({...pboxp, wprice:pboxp.wprice-w[e.target.id.substr(1)].whprice});
        for(let i=0; i<dibData.length; i=i+1){
        setDibData(dibData.filter(dibData => dibData.dwhidx!==w[e.target.id.substr(1)].whidx ));
        }
        console.log(dibData);
      }

  }
  
  const clicksItem = (e) => {
    if(id===undefined || id===null || id===""){
      window.alert("로그인 후 이용 가능한 서비스입니다.");
      return;
    }
    
    if(e.target.type==="submit"){
      let btnconfirm= window.confirm("찜하시겠습니까?");
      console.log(btnconfirm);
      if(btnconfirm===false){
        return;
      }else if(btnconfirm===true){
        setDibData([...dibData,{id:nextId.current ,dtype:"스드메", dmid:id, dsidx:s[e.target.id.substr(1)].sidx}]);
      }
      console.log(dibData);
      console.log(pboxp);
      setA(true);
      return;
    }


    const sc = document.getElementById("sd"+e.target.id.substr(1));
    console.log(e);
    console.log("sc1 체크여부 :"+sc.checked+"아이디: s"+e.target.id.substr(1));
    if(sc.checked==false){
      e.target.style.opacity=0.1;
        setPboxp({...pboxp, sprice:pboxp.sprice+s[e.target.id.substr(1)].sprice});
        setDibData([...dibData,{id:nextId.current ,dtype:"스드메", dmid:id, dsidx:s[e.target.id.substr(1)].sidx}]);
    }else{
      e.target.style.opacity=0;
        setPboxp({...pboxp, sprice:pboxp.sprice-s[e.target.id.substr(1)].sprice});
        for(let i=0; i<dibData.length; i=i+1){
          setDibData(dibData.filter(dibData => dibData.dsidx!==s[e.target.id.substr(1)].sidx ));
          }
    }
  }

  const clickpItem = (e) => {
    if(id===undefined || id===null || id===""){
      window.alert("로그인 후 이용 가능한 서비스입니다.");
      return;
    }
    
    if(e.target.type==="submit"){
      let btnconfirm= window.confirm("찜하시겠습니까?");
      console.log(btnconfirm);
      if(btnconfirm===false){
        return;
      }else if(btnconfirm===true){
        setDibData([...dibData,{id:nextId.current ,dtype:"플래너", dmid:id, dpidx:p[e.target.id.substr(1)].pidx}]);
      }
      console.log(dibData);
      console.log(pboxp);
      setA(true);
      return;
    }


    const pc = document.getElementById("pd"+e.target.id.substr(1));
    console.log("pcpc"+e.target.id.substr(1))
    console.log("pc1 체크여부 :"+pc.checked+"아이디: pd"+e.target.id.substr(1))
    if(pc.checked==false){
      e.target.style.opacity=0.1;
        setPboxp({...pboxp, pprice:pboxp.pprice+p[e.target.id.substr(1)].pprice});
        setDibData([...dibData,{id:nextId.current ,dtype:"플래너", dmid:id, dpidx:p[e.target.id.substr(1)].pidx}]);
    }else{
      e.target.style.opacity=0;
        setPboxp({...pboxp, pprice:pboxp.pprice-p[e.target.id.substr(1)].pprice});
        for(let i=0; i<dibData.length; i=i+1){
          setDibData(dibData.filter(dibData => dibData.dpidx!==p[e.target.id.substr(1)].pidx ));
        }
    }
  }

  const clickhItem = (e) => {
    if(id===undefined || id===null || id===""){
      window.alert("로그인 후 이용 가능한 서비스입니다.");
      return;
    }
    
    if(e.target.type==="submit"){
      let btnconfirm= window.confirm("찜하시겠습니까?");
      console.log(btnconfirm);
      if(btnconfirm===false){
        return;
      }else if(btnconfirm===true){
        setDibData([...dibData,{id:nextId.current ,dtype:"허니문", dmid:id, dhidx:h[e.target.id.substr(1)].hidx}]);
      }
      console.log(dibData);
      console.log(pboxp);
      setA(true);
      return;
    }


    const hc = document.getElementById("ho"+e.target.id.substr(1));
    if(hc.checked==false){
      e.target.style.opacity=0.1;
        setPboxp({...pboxp, hprice:pboxp.hprice+h[e.target.id.substr(1)].hcost});
        setDibData([...dibData,{id:nextId.current ,dtype:"허니문", dmid:id, dhidx:h[e.target.id.substr(1)].hidx}]);
    }else{
        e.target.style.opacity=0;
        setPboxp({...pboxp, hprice:pboxp.hprice-h[e.target.id.substr(1)].hcost});
        for(let i=0; i<dibData.length; i=i+1){
          setDibData(dibData.filter(dibData => dibData.dhidx!==h[e.target.id.substr(1)].hidx ));
        }
    }
  }
  const wItem = w?.map((wlist,a) => {
    return (
      <div data-aos="fade-up" style={{ }}>
      <FlexBox style={{width:"100%"}}>
      <div
      style={{
        width: '1395px',
        height: '550px',
        backgroundImage: `url(upload/${wlist.whimg2})`,
        backgroundSize: '1395px 550px',
        borderRadius: "7px"
      }}/>
      <div className='ehover' onClick={() => window.open('/collect/wedding-hall/', '_blank')}>{wlist.whstr}</div>
      </FlexBox>
      { pboxp.wprice !== 0 ?
      <><input type="checkBox" id={"w"+a} style={{display:"none"}}/><label htmlFor={'w'+a} id={"a"+a} className='pcheck' onClick={(e)=>clickwItem(e)}></label></>:<><input type="checkBox" checked={false} id={'w'+a} style={{display:"none"}}/><label htmlFor={'w'+a} id={"a"+a} className='pcheck' style={{opacity:0}} onClick={(e)=>clickwItem(e)}></label></>}
    <p style={{ marginTop: 10, marginBottom: "50px"}}>
      <Typhography size="md" font="medium" style={{display:"inline-block", width:"100%", padding:"20px 10px 25px 20px", borderBottom:"1px dotted lightGray"}}>
        <span key={a} style={{fontSize:"25px", fontWeight:'bold'}}>{wlist.whname}</span>
        <div style={{float:"right"}}>
        <span style={{fontSize:"25px", fontWeight:'bold', lineHeight:"65px", marginRight:"100px"}}>{comma(wlist.whprice)}만원</span>
          <Payment ptext={"예약하기💕"} width={"120px"} height={"100px"} wlist={wlist} background ={'#C3B6D9'} borderRadius={'10px'}></Payment>
          <Button id={"w"+a} onClick={(e)=>{clickwItem(e)}} style={{width:120, height:100, background:"lightgray", borderRadius:'10px', marginLeft:'10px'}}>찜하기💕</Button>
        </div>
        <span style={{fontSize:"20px", fontWeight:'bold', lineHeight:"40px"}}><br/>{wlist.whkind}</span>
      </Typhography>
    </p>
    </div>);
  })
  console.log(w);
  const sItem = s?.map((slist,b) => {
    return (
      <div data-aos="fade-up" style={{}}>
      <FlexBox style={{width:"700px" }}>
      <div
      style={{
        width: '650px',
        height: '350px',
        backgroundImage: `url(upload/${slist.simg2})`,
        backgroundSize: '650px 350px',
        borderRadius: "7px"
      }}/>
      <div className='ehover2' onClick={() => window.open('/collect/sdm/', '_blank')}>{slist.sstr}</div>
      </FlexBox>
      { pboxp.sprice !== 0 ?
      <><input type="checkbox" id={"sd"+b} style={{display:"none"}}/><label htmlFor={'sd'+b} id={"b"+b} className='ppcheck' onClick={(e)=>clicksItem(e)}></label></>:<><input type="checkbox" checked={false} id={"sd"+b} style={{display:"none"}}/><label htmlFor={"sd"+b} id={"b"+b} className='ppcheck' style={{}} onClick={(e)=>clicksItem(e)}></label></>}
    <p style={{ marginTop: 10, marginBottom: "50px" }}>
      <Typhography size="md" font="medium" style={{display:"inline-block", width:"92%", padding:"10px 0px 15px 20px", borderBottom:"1px dotted lightGray"}}>
        <span key={b} style={{fontSize:"23px", fontWeight:'bold'}}>{slist.scomp}</span>
        <div style={{float:"right"}}>
        <span style={{fontSize:"23px", fontWeight:'bold', lineHeight:"55px", marginRight:"10px"}}>{comma(slist.sprice)}만원</span>
          <Payment ptext={"예약하기💕"} width={"120px"} height={"100px"} slist={slist} background ={'#C3B6D9'} borderRadius={'10px'}></Payment>
          <Button id={"b"+b}  onClick={(e)=>{clicksItem(e)}} style={{width:120, height:100, background:"lightgray", borderRadius:'10px', marginLeft:'10px'}}>찜하기💕</Button>
        </div>
        <span style={{fontSize:"19px", fontWeight:'bold', lineHeight:"40px"}}><br/>{slist.slocation}</span>
      </Typhography>
    </p>
    </div>);
  })
  
  const pItem = p?.map((plist,c) => {
    return (
      <div data-aos="fade-up" style={{ }}>
      <FlexBox style={{width:"700px"}}>
      <div
      style={{
        width: '650px',
        height: '600px',
        backgroundImage: `url(upload/${plist.pimg})`,
        backgroundSize: '650px 600px',
        borderRadius: "7px"
      }}/>
      <div className='ehover3' onClick={() => window.open('/collect/honeymoon/', '_blank')}>{plist.pstr}</div>
      </FlexBox>
      { pboxp.pprice !==0 ?
     <><input type="checkbox" id={"pd"+c} style={{display:"none"}}/><label htmlFor={'pd'+c} id={"c"+c} className='ppcheck' onClick={(e)=>clickpItem(e)}></label></>:<><input type="checkbox" checked={false} id={"pd"+c} style={{display:"none"}}/><label htmlFor={"pd"+c} id={"c"+c} className='ppcheck' style={{opacity:0}} onClick={(e)=>clickpItem(e)}></label></>}
    <p style={{ marginTop: 10, marginBottom: "50px" }}>
      <Typhography size="md" font="medium" style={{display:"inline-block", width:"92%", padding:"10px 0px 15px 20px", borderBottom:"1px dotted lightGray"}}>
        <span key={c} style={{fontSize:"23px", fontWeight:'bold'}}>{plist.pname}</span>
        <div style={{float:"right"}}>
          <span style={{fontSize:"23px", fontWeight:'bold', lineHeight:"55px", marginRight:"10px"}}>{comma(plist.pprice)}만원</span>
          <Payment ptext={"예약하기💕"} width={"120px"} height={"100px"} plist={plist} background ={'#C3B6D9'} borderRadius={'10px'}></Payment>
          <Button  onClick={(e)=>{clickpItem(e)}} id={"c"+c} style={{width:120, height:100, background:"lightgray", borderRadius:'10px', marginLeft:'10px'}}>찜하기💕</Button>
        </div>
        <span style={{fontSize:"19px", fontWeight:'bold', lineHeight:"40px"}}><br/>{plist.pphone}</span>
      </Typhography>
    </p>
    </div>);
  })
  const hItem = h?.map((hlist,d) => {
    console.log(d);
    console.log(`url(upload/${hlist.himg})`);
    return (
      <div data-aos="fade-up" style={{ }}>
      <FlexBox style={{width:"100%"}}>
      <div
      style={{
        width: '1395px',
        height: '550px',
        backgroundImage: `url('upload/${hlist.himg2}')`,
        backgroundSize: '1395px 550px',
        backgroundRepeat : "no-repeat",
        borderRadius: "7px"
      }} />
      <div className='ehover' style={{overflow:"hidden"}} onClick={() => window.open('/collect/honeymoon/', '_blank')}>{hlist.hstr}</div>
      </FlexBox>
      { pboxp.hprice !=0 ?
       <><input type="checkBox" id={"ho"+d} style={{display:"none"}}/><label htmlFor={'ho'+d} id={"d"+d} className='pcheck' onClick={(e)=>clickhItem(e)}></label></>:<><input type="checkBox" checked={false} id={'ho'+d} style={{display:"none"}}/><label htmlFor={'ho'+d} id={"d"+d} className='pcheck' style={{opacity:0}} onClick={(e)=>clickhItem(e)}></label></>}
    <p style={{ marginTop: 10, marginBottom: "50px" }}>
      <Typhography size="md" font="medium" style={{display:"inline-block", width:"100%", padding:"20px 10px 25px 20px", borderBottom:"1px dotted lightGray"}}>
        <span key={d} style={{fontSize:"25px", fontWeight:'bold'}}>{hlist.hlocation}</span>
        <div style={{float:"right"}}>
        <span style={{fontSize:"25px", fontWeight:'bold', lineHeight:"65px", marginRight:"100px"}}>{comma(hlist.hcost)}만원</span>
          <Payment ptext={"예약하기💕"} width={"120px"} height={"100px"} hlist={hlist} background ={'#C3B6D9'} borderRadius={'10px'}></Payment>
          <Button  onClick={(e)=>{clickhItem(e)}} id={"d"+d} style={{width:120, height:100, background:"lightgray", borderRadius:'10px', marginLeft:'10px'}}>찜하기💕</Button>
        </div>
        <span style={{fontSize:"20px", fontWeight:'bold', lineHeight:"40px"}}><br/>{hlist.hbrand}</span>
      </Typhography>
    </p>
    </div>);
  })

  console.log("스드메"+sItem);
  console.log(pItem);
  console.log("허니문"+hItem);

  const [dibData, setDibData] = useState([]);
  console.log("")
  useEffect(()=> {
    console.log(dibData);
  },[dibData])

  useEffect(()=>{
    console.log(dibData);
    if(a===true){
      dibBtn();
    }
  },[a])


  return (
    <div style={{marginBottom:80, marginTop:70}}>
      {(wItem !== undefined && wItem?.length!==0) ? 
      <>
      <h1 style={{marginTop:"-50px",marginBottom:"40px", marginLeft:"10px"}}>웨딩홀</h1> 
      <div style={{marginBottom:"80px", display:"flex", flexWrap:"wrap"}}>{wItem}</div></>: null }
      {(sItem !== undefined && sItem?.length!==0) ?
      <>
      <h1 style={{marginTop:"-50px",marginBottom:"40px", marginLeft:"10px"}}>스드메</h1> 
      <div style={{marginBottom:"80px", display:"flex", flexWrap:"wrap"}}>{sItem}</div></>: null }
      {pItem !== undefined && pItem?.length!==0 ? 
      <>
      <h1 style={{marginBottom:"40px", marginLeft:"10px"}}>플래너</h1>
      <div style={{marginBottom:"80px", display:"flex", flexWrap:"wrap"}}>{pItem}</div></>: null }
      {hItem !== undefined && hItem?.length!==0 ? 
      <>
      <h1 style={{marginBottom:"40px", marginLeft:"10px"}}>허니문</h1>
      <div style={{marginBottom:"80px", display:"flex", flexWrap:"wrap"}}>{hItem}</div></>: null }
      { pboxp.wprice+pboxp.sprice+pboxp.pprice+pboxp.hprice != 0 ?  <>
        {tbox == 0 ? 
        <div id="pricebox" style={{background:"rgb(255, 252, 253)", opacity:"1" ,color:"black" ,height:365, width:400, position:"fixed", right:"100px", bottom:"50px", transition: "all 1s", fontSize:"20px", borderRadius:"10px"}}><div style={{width:"90%", margin:"0 auto", lineHeight:"50px", marginTop:"15px"}}><div onClick={clickTbox} style={{width:"20px", height:"20px", cursor:"pointer", position:"absolute", right:"-30px"}}>X</div><span style={{marginLeft:"10px"}}>웨딩홀</span><span style={{float:"right"}}>{comma(pboxp.wprice)}만원</span></div><div style={{width:"90%", margin:"0 auto", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>스드메</span><span style={{float:"right"}}>{comma(pboxp.sprice)}만원</span></div><div style={{width:"90%", margin:"0 auto", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>플래너</span><span style={{float:"right"}}>{comma(pboxp.pprice)}만원</span></div><div style={{width:"90%", height:"60px" ,borderBottom:"2px solid", margin:"0 auto", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>허니문</span> <span style={{float:"right"}}>{comma(pboxp.hprice)}만원</span></div><div style={{color:"red", width: "90%", margin:"0 auto", marginTop:"10px", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>합계 </span><span style={{float:"right"}}>{comma(pboxp.wprice+pboxp.sprice+pboxp.pprice+pboxp.hprice)}만원</span></div><div className='dib1' onClick={dibBtn}>전체 찜하기💕</div></div> : <div className='dib2' onClick={clickTbox2} style={{position:"fixed", bottom:"280px", right:"18px", fontSize:"40px"}}>💌</div>}</>:
      <><div id="pricebox" style={{background:"rgb(255, 248, 248)", opacity:"1" ,color:"black" ,height:365, width:400, position:"fixed", bottom:"50px", right:"-400px", transition: "all 1s", fontSize:"20px", borderRadius:"10px"}}><div style={{width:"90%", margin:"0 auto", lineHeight:"50px", marginTop:"15px"}}><div onClick={clickTbox} style={{width:"20px", height:"20px", cursor:"pointer", position:"absolute", right:"-30px"}}>X</div><span style={{marginLeft:"10px"}}>웨딩홀</span><span style={{float:"right"}}>{comma(pboxp.wprice)}만원</span></div><div style={{width:"90%", margin:"0 auto", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>스드메</span><span style={{float:"right"}}>{comma(pboxp.sprice)}만원</span></div><div style={{width:"90%", margin:"0 auto", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>플래너</span><span style={{float:"right"}}>{comma(pboxp.pprice)}만원</span></div><div style={{width:"90%", height:"60px" ,borderBottom:"2px solid", margin:"0 auto", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>허니문</span> <span style={{float:"right"}}>{comma(pboxp.hprice)}만원</span></div><div style={{color:"red", width: "90%", margin:"0 auto", marginTop:"10px", lineHeight:"50px"}}><span style={{marginLeft:"10px"}}>합계 </span><span style={{float:"right"}}>{comma(pboxp.wprice+pboxp.sprice+pboxp.pprice+pboxp.hprice)}만원</span></div><div className='dib1'>전체 찜하기💕</div></div>
      </>}
      </div>
  )
}

export default EstimateItem;
```
- #### 검색 결과<br>
받아온 data들을 정렬해서 띄워주고 상품을 클릭하면 선택한 상품들의 계산서가 나타나며 각 상품 찜하기, 선택 상품 찜하기 , 예약하기(결제(아임포트 결제 api 사용))를 할 수 있습니다.<br>


- #### 검색 후 하단 결과 화면<br><br>
<img width="1108" alt="검색 결과" src="https://user-images.githubusercontent.com/117880554/224939593-c3bfec30-0c0a-4889-bf0a-f4f2debf3ada.png">
## Likes.jsx 컴포넌트

※ 찜하기
```javascript

export default () => {
  const comma = (num) =>[num].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
  const id = sessionStorage.getItem("mid");
  const nav = useNavigate();
    const inputBorder= useRef();
  const [dibData,setDibData] = useState([{}]);
  useEffect(()=>{
    axios.post("/searchDib", null, {params:{mid:id}})
    .then((res)=>{
      console.log(res.data);
      setDibData(res.data);
    })
  },[])
  
  const [likes, setLikes] = useState([
    // {name: "gd"},
    // {name: "gd"},
    // {name: "gd"},
  ])
  console.log(dibData);
  const {wh,sd,pl,ho} = dibData;
  useEffect(()=>{
    console.log(wh);
    let ls = [];
    if(wh!==undefined){
      for(let i=0; i<wh.length; i++){
        ls.push({dname: wh[i].whname, dtype: "웨딩홀", dprice: wh[i].whprice ,dwhidx:wh[i].whidx, dmid:id, bprice: wh[i].bprice ,dorder: i});
        setLikes(ls);
      }
    }
      if(sd!==undefined){
        for(let i=0; i<sd.length; i++){
          ls.push({dname: sd[i].scomp, dtype: "스드메", dprice: sd[i].sprice ,dsidx:sd[i].sidx, dmid:id, dorder: wh.length+i,});
          setLikes(ls);
        }
      }
      if(pl!==undefined){
        for(let i=0; i<pl.length; i++){
          ls.push({dname: pl[i].pname, dtype: "플래너", dprice: pl[i].pprice ,dpidx:pl[i].pidx, dmid:id, dorder: wh.length+sd.length+i,});
          setLikes(ls);
        }
      }
      if(ho!==undefined){
        for(let i=0; i<ho.length; i++){
          ls.push({dname: ho[i].hlocation, dtype: "허니문", dprice: ho[i].hcost ,dhidx:ho[i].hidx, dmid:id, dorder: wh.length+sd.length+pl.length+i,});
          setLikes(ls);
        }
      }
  },[wh],[sd],[pl],[ho]);
  // console.log({a})
  // likes.concat();
  // for(let i=1; i<3; i++){
  //   likes.concat({name: dd[i]});
  // }
  // console.log(likes)
  const [delData, setdelData] = useState([]);
  const [delbtn, setDelbtn] = useState(false);

  // const onRemoveHandler = (id) => () => {
  //   if (!window.confirm(`${likes[id].name} 을 찜 목록에서 삭제하시겠습니까?`)) return


  // }
  const [showData,setShowData]=useState([]);;
  useEffect(()=>{
    let tempShow = []
    console.log(likes);
    tempShow=likes.slice();
    console.log(tempShow)
      for(let i =0; i<tempShow.length; i++){
        tempShow[i]={...tempShow[i], dprice:comma(tempShow[i].dprice)}
    }
    setShowData(tempShow);
    console.log(showData);
  },[likes])


  useEffect(()=>{
    console.log("여기요오오"+delData);
    if(delbtn===true){
      axios.post("/deleteDib", delData)
      .then((res)=>{
        window.alert("힝 삭제됐어");
        setDelbtn(false);
        nav(0);
      });  
    }


    //버튼누를때 유즈스테이트 하나 바뀌게해서 만약에 그값이 바뀌면 axios 보낸다 해주면될듯
  },[delData,delbtn]);

  const [checkall,setCheckall] = useState(false);
  const [checkList, setCheckList] = useState([]);
  // useEffect(()=>{
  //   console.log(delData,checkall);
  // },[delData,checkall])
  let tempdelData = [];
  let tempcheckList = [];
  let tempallData= [];
  const onCheckboxChangeHandler = (e,index) => {
    console.log(checkList.length, likes.length);
    console.log(index);
    if (e.target.name!=="rperson" && e.target.name!=="rdatestart" && e.target.name!=="rdateend"){
      const val = Number(e.target.value)
      setCheckList(checkList.includes(val) ? checkList.filter((v) => v !== val) : [...checkList, val])
      console.log(val);
      console.log(checkList);
      {val ===-1&&checkall===false ? setCheckall(true): setCheckall(false)};
      if(val===-1&&delData.length!==likes.length){
        setCheckList([]);
        setdelData([]);
        setdelData(likes);
        console.log("제바아아알")
        console.log(delData);
        return;
      }else if(val===-1){
        // setCheckList(checkList.filter(v=> v !== val));
        setCheckall(false);
        setdelData([]);
        console.log(delData);
        return;
      }else if (val!==-1&&delData.length===likes.length){
        setCheckall(false);
        console.log(delData);
        console.log(checkList);
        for(let i = 0 ; i<likes.length; i++){
          tempcheckList.push(i);
        }
        tempcheckList.splice(val,1);
        setCheckList(tempcheckList);
        tempallData = delData.slice();
        tempallData.splice(val,1);
        setdelData(tempallData);
        return;
      }



      
      console.log(e.target.checked,checkall)
      console.log(likes[e.target.value].dtype, e.target.checked, checkall)
      if(likes[e.target.value].dtype==="웨딩홀"&&e.target.checked===true &&checkall===false){
        setdelData([...delData,{
          dtype:"웨딩홀",
          dmid:id,
          dwhidx:likes[e.target.value].dwhidx,
          dprice:likes[e.target.value].dprice,
          dname:likes[e.target.value].dname,
          dorder: index,
          bprice: likes[e.target.value].bprice
      }])}else if(likes[e.target.value].dtype==="웨딩홀"&&e.target.checked===false &&checkall===false){
        setdelData(delData.filter(delData=>delData.dwhidx!==likes[e.target.value].dwhidx))
      }
      if(likes[e.target.value].dtype==="스드메"&&e.target.checked===true &&checkall===false){
        console.log(likes[e.target.value].dsidx);
        setdelData([...delData,{
          dtype:"스드메",
          dmid:id,
          dsidx:likes[e.target.value].dsidx,
          dprice:likes[e.target.value].dprice,
          dname:likes[e.target.value].dname,
          dorder:index,
      }])}else if(likes[e.target.value].dtype==="스드메"&&e.target.checked===false &&checkall===false){
        setdelData(delData.filter(delData=>delData.dsidx!==likes[e.target.value].dsidx))
      }
      if(likes[e.target.value].dtype==="플래너"&&e.target.checked===true &&checkall===false){
        console.log(likes[e.target.value].dpidx);
        setdelData([...delData,{
        dtype:"플래너",
        dmid:id,
        dpidx:likes[e.target.value].dpidx,
        dprice:likes[e.target.value].dprice,
        dname:likes[e.target.value].dname,
        dorder:index,
      }])}else if(likes[e.target.value].dtype==="플래너"&&e.target.checked===false &&checkall===false){
        setdelData(delData.filter(delData=>delData.dpidx!==likes[e.target.value].dpidx))
      }
      if(likes[e.target.value].dtype==="허니문"&&e.target.checked===true &&checkall===false){
        console.log(likes[e.target.value].dhidx);
        setdelData([...delData,{
        dtype:"허니문",
        dmid:id,
        dhidx:likes[e.target.value].dhidx,
        dprice:likes[e.target.value].dprice,
        dname:likes[e.target.value].dname,
        dorder:index,
      }])}else if(likes[e.target.value].dtype==="허니문"&&e.target.checked===false &&checkall===false){
        setdelData(delData.filter(delData=>delData.dhidx!==likes[e.target.value].dhidx))
      }
    }


    if (e.target.name==="rperson" || e.target.name==="rdatestart" || e.target.name==="rdateend"){
      tempdelData=delData.slice();
      // console.log(delData.findIndex(d=>d.dorder===index));
      if(tempdelData.length!==0 &&e.target.name==="rperson"){
      tempdelData[delData.findIndex(d=>d.dorder===index)]={...tempdelData[delData.findIndex(d=>d.dorder===index)],[e.target.name]:parseInt(e.target.value)};
      setdelData(tempdelData);
      } else if(tempdelData.length!==0 &&e.target.name!=="rperson"){
        tempdelData[delData.findIndex(d=>d.dorder===index)]={...tempdelData[delData.findIndex(d=>d.dorder===index)],[e.target.name]:e.target.value};
        setdelData(tempdelData);
        }
      console.log(tempdelData);
      console.log(index);
      console.log(checkall)
    }
  }

  const borderChange = (e)=> {
    inputBorder.current.style.border="1px solid lightGray";
    inputBorder.current = e.target;
    inputBorder.current.style.border="1px solid black";
  }
  const personRegExp = /^[0-9]{0,4}$/;
  const dataConfirm= (e) =>{
    if(!personRegExp.test(inputBorder.current.value)){
      window.alert("0명 이상 입력해주세요");
      inputBorder.current.value="";
    }
  }
  console.log(delData);
  return (
    <div style={{ width: '100%' }}>
      <Table
        columns={[
          {
            name: checkall === false ? <input type="checkBox" checked={false} value={-1} onChange={(e)=>onCheckboxChangeHandler(e)}/>:<input type="checkBox" checked={true} value={-1} onChange={(e)=>onCheckboxChangeHandler(e)}/>,
            render: (v, index) => (
              checkall === true ? <input type="checkbox" value={index} onChange={(e)=>onCheckboxChangeHandler(e,index)} checked/> : checkall === false && checkList.indexOf(index) !== -1 ? <input type="checkbox" value={index} onChange={(e)=>onCheckboxChangeHandler(e,index)} checked/>:<input type="checkbox" value={index} onChange={(e)=>onCheckboxChangeHandler(e,index)}/>
            ),
          },
          {
            name: '등록번호',
            render: (v, index) => index + 1,
            style: {
              width: 80,
            },
          },
          {
            name: '타입',
            id: 'dtype',
          },
          {
            name: '상품명',
            id: 'dname',
          },
          {
            name: '예약일 선택',
            render: (v,index) => ( checkall===false ?( likes[index].dtype !== "허니문" && checkList.indexOf(index) === -1 ? <input type="date" name="rdatestart" onChange={(e)=>onCheckboxChangeHandler(e, index)} style={{width:"300px", fontSize:"16px", textAlign:"center", border:"none"}} disabled/> : likes[index].dtype !== "허니문" && checkList.indexOf(index) !== -1 ? <input type="date" name="rdatestart" onChange={(e)=>onCheckboxChangeHandler(e, index)} style={{width:"300px", fontSize:"16px", textAlign:"center", border:"none"}}/> : checkList.indexOf(index) === -1 ? <><input type="date" disabled onChange={(e)=>onCheckboxChangeHandler(e,index)} name="rdatestart" style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/><span> ~ </span><input type="date" name='rdateend' disabled onChange={(e)=>onCheckboxChangeHandler(e,index)} style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/></> :  <><input type="date" onChange={(e)=>onCheckboxChangeHandler(e,index)} name="rdatestart" style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/><span> ~ </span><input type="date" name='rdateend' onChange={(e)=>onCheckboxChangeHandler(e,index)} style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/></>)
            :( likes[index].dtype !== "허니문" ? <input type="date" name="rdatestart" onChange={(e)=>onCheckboxChangeHandler(e, index)} style={{width:"300px", fontSize:"16px", textAlign:"center", border:"none"}}/> : <><input type="date" onChange={(e)=>onCheckboxChangeHandler(e,index)} name="rdatestart" style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/><span> ~ </span><input type="date" name='rdateend' onChange={(e)=>onCheckboxChangeHandler(e,index)} style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/></>)),
            id: 'selectRdate',
          },
          {
            name: '1인 식대',
            render: (v,index) => likes[index].dtype === "웨딩홀"?<div type="text" name="bprice" style={{width:"50px", textAlign:"center"}}>{likes[index].bprice} 만원</div>: null,
            id: 'bprice',
          },
          {
            name: '인원 선택',
            render: (v,index) => ( checkall===false ?( likes[index].dtype === "웨딩홀" && checkList.indexOf(index) === -1 ?<><input type="text" disabled ref={inputBorder} onClick={(e)=>borderChange(e)} onChange={(e)=>{onCheckboxChangeHandler(e,index);dataConfirm(e)}} name="rperson" maxLength="4" style={{width:"50px", border:"1px solid lightGray", textAlign:"center"}}/><label style={{color:"black", marginLeft:"10px"}}>명</label></> : likes[index].dtype === "웨딩홀" && checkList.indexOf(index) !== -1 ?  <><input type="text" ref={inputBorder} onClick={(e)=>borderChange(e)} onChange={(e)=>{onCheckboxChangeHandler(e,index);dataConfirm(e)}} name="rperson" maxLength="4" style={{width:"50px", border:"1px solid lightGray", textAlign:"center"}}/><label style={{color:"black", marginLeft:"10px"}}>명</label></>:null)
            : ( likes[index].dtype === "웨딩홀" ?  <><input type="text" ref={inputBorder} onClick={(e)=>borderChange(e)} onChange={(e)=>{onCheckboxChangeHandler(e,index);dataConfirm(e)}} name="rperson" maxLength="4" style={{width:"50px", border:"1px solid lightGray", textAlign:"center"}}/><label style={{color:"black", marginLeft:"10px"}}>명</label></>:null)),
            id: 'selectPopu',
          },
          {
            name: '가격',
            render: (v,index) => likes[index].dtype === "웨딩홀" && (delData[delData.findIndex(d=>d.dorder===index)]?.rperson ===null || delData[delData.findIndex(d=>d.dorder===index)]?.rperson === undefined || delData[delData.findIndex(d=>d.dorder===index)]?.rperson === "")?<div type="text" name="dprice" style={{width:"100px", textAlign:"right"}}>{likes[index]?.dprice} 만원</div>: likes[index].dtype === "웨딩홀"&&(checkList.indexOf(index) !==-1||checkall)&&(delData[delData.findIndex(d=>d.dorder===index)]?.rperson !==null || delData[delData.findIndex(d=>d.dorder===index)]?.rperson !==undefined || delData[delData.findIndex(d=>d.dorder===index)]?.rperson !== "") ?<div type="text" name="dprice" style={{width:"100px", textAlign:"right"}}>{likes[index].dprice+delData[delData.findIndex(d=>d.dorder===index)].bprice*delData[delData.findIndex(d=>d.dorder===index)].rperson} 만원</div> : <div type="text" name="dprice" style={{width:"100px", textAlign:"right"}}>{likes[index].dprice} 만원</div>,
            id: 'dprice',
          },
        ]}
        dataSource={showData}
      />
      <div style={{float:"right", marginTop:'50px', width:200, display:"flex", justifyContent:"space-around"}}>
        <Button onClick={()=>setDelbtn(true)}>선택삭제</Button>
      <Payment ptext="결제하기" pData={delData} />
      </div>
    </div>
  )
}
```
'찜하기' 버튼을 클릭 해 선택한 상품 백으로 보내줍니다.

## Back_DibController
```java
@RestController
@Log
public class DibController {

    @Autowired
    private DibService  dServ;

    @PostMapping("/ddibInsert")
    public String ddibInsert (@RequestBody List<Dib> dibData){
        log.info("ddibInsert()");
        log.info("띱"+dibData);
        return dServ.ddibInsert(dibData);
    }
}
## Back_DibService
```java
@Service
@Log
public class DibService {
    @Autowired
    private DibRepository dRepo;
    @Autowired
    private WeddingHoleRepository whRepo;
    @Autowired
    private SDMRepository sRepo;
    @Autowired
    private PlannerRepository pRepo;
    @Autowired
    private HoneyMoonRepository hRepo;
    public String ddibInsert(List<Dib> dibData) {
        String res = null;
        try{
            for(Dib dList : dibData){
                dRepo.save(dList);
            }
            res="Success";
        }catch(Exception e){
            e.printStackTrace();
            res="Failed";
        }

        return res;
    }
}
```
프론트에서 보낸 값을 database에 저장해줍니다.<br><br>

- #### 상품 선택 후 화면<br><br>
<img width="1107" alt="검색후 클릭" src="https://user-images.githubusercontent.com/117880554/224940581-64c31841-f5d8-4a81-a4fc-fd3c1bbd744b.png">

- #### 선택 상품 찜한 후 화면<br><br>
<img width="1107" alt="화면 찜하기" src="https://user-images.githubusercontent.com/117880554/224940594-71d16e58-b38e-47a5-a124-929e63ddce38.png">

- #### 계산서를 닫았을 때 우측 하단 아이콘<br><br>
<img width="48" alt="계산서 축소 아이콘" src="https://user-images.githubusercontent.com/117880554/224941238-81895536-32f3-4709-bf0e-e6eb7967df5a.png">
※ 결제하기

```javascript

const Payment = ({ effect, deps, ptext, width, height, zIndex, wlist, slist, plist, hlist, pData,borderRadius,background,...props }) => {
  const nav = useNavigate();
  useEffect(() => {
    const jquery = document.createElement("script");
    jquery.src = "https://code.jquery.com/jquery-1.12.4.min.js";
    const iamport = document.createElement("script");
    iamport.src = "https://cdn.iamport.kr/js/iamport.payment-1.1.7.js";
    document.head.appendChild(jquery);
    document.head.appendChild(iamport);
    return () => {
        document.head.removeChild(jquery); document.head.removeChild(iamport);
    }
  }, []);
  const id = sessionStorage.getItem("mid");
  const name = sessionStorage.getItem("mname");
  const phone = sessionStorage.getItem("mphone");
  const [data, setData] = useState({
    pg: 'html5_inicis.INIpayTest', // PG사 (필수항목)
    pay_method: 'card', // 결제수단 (필수항목)
    merchant_uid: `mid_${new Date().getTime()}`, // 결제금액 (필수항목)
    name: '결제 테스트', // 주문명 (필수항목)
    amount: '100', // 금액 (필수항목)
    custom_data: { name: '부가정보', desc: '세부 부가정보' },
    buyer_name: name, // 구매자 이름
    buyer_tel: phone, // 구매자 전화번호 (필수항목)
    buyer_email: null, // 구매자 이메일
    buyer_addr: null,
    buyer_postalcode: null,
  });

  const [reservData,setReservData] = useState([])
    

    useEffect(()=>{
      console.log("피데이터"+pData);
      console.log(pData);
      if(pData===undefined||pData.length===0){
        return;
      }
      if(pData!==undefined&&pData.length!==0){
        let tprice=0;
        for(let i =0; i<pData.length; i++){
          if(pData[i].dtype==="웨딩홀"){
            // for(let i =0; i<pData.length; i++){
              tprice=tprice+pData[i].dprice+pData[i].bprice*pData[i]?.rperson;
            // }
            console.log(pData[i].bprice);
          }else {
              tprice=tprice+pData[i].dprice;
        }
        }
        if(pData.length>1){
          console.log(tprice);
        setData({...data,
          amount:tprice,
          name: pData[0].dname+" 외"+(pData.length-1).toString()+"건",
        })}
        else if(pData.length===1){
          setData({...data,
            amount:tprice,
            name: pData[0].dname,
          })
        }
        console.log(tprice);

      }
        console.log(data.name)
      },[pData]);
  
    useEffect(()=>{
        if(wlist!==undefined){
        setData({...data,
          name:wlist.whname,
          amount:wlist.whprice,
        })}
    },[wlist]);
    
    useEffect(()=>{
      if(slist!==undefined){
      setData({...data,
        name:slist.scomp,
        amount:slist.sprice,
      })}
    },[slist]);

    useEffect(()=>{
      if(plist!==undefined){
      setData({...data,
        name:plist.pname,
        amount:plist.pprice,
      })}
  },[plist]);

    useEffect(()=>{
      if(hlist!==undefined){
      setData({...data,
        name:hlist.hlocation,
        amount:hlist.hcost,
      })}
    },[hlist]);

    let fiData = [];
    const [paybtn, setPayBtn]=useState(false);
    useEffect(()=>{
      if(reservData?.length===0||reservData===undefined||reservData?.length>pData?.length){
        return;
      }

      for(let i=0; i<pData?.length; i++){
        if(pData[i]?.dtype==="웨딩홀"){
            fiData.push({
            rwhidx: pData[i].dwhidx,
            rcost: pData[i].dprice,
            rmid:id,
            rimpuid: reservData[0].rimpuid,
            rtype:"웨딩홀",
            rstatus : "진행예정",
            rdatestart : pData[i].rdatestart,
            rperson : pData[i].rperson
          })}else if(pData[i]?.dtype==="스드메"){
            fiData.push({
            rsidx: pData[i].dsidx,
            rcost:pData[i].dprice,
            rmid:id,
            rimpuid: reservData[0].rimpuid,
            rtype:"스드메",
            rstatus : "진행예정",
            rdatestart : pData[i].rdatestart,
          })}else if(pData[i]?.dtype==="플래너"){
            fiData.push({
            rpidx: pData[i].dpidx,
            rcost:pData[i].dprice,
            rmid:id,
            rimpuid: reservData[0].rimpuid,
            rtype:"플래너",
            rstatus : "진행예정",
            rdatestart : pData[i].rdatestart,
          })}else if(pData[i]?.dtype==="허니문"){
            fiData.push({
            rhidx: pData[i].dhidx,
            rcost:pData[i].dprice,
            rmid:id,
            rimpuid: reservData[0].rimpuid,
            rtype:"허니문",
            rstatus : "진행예정",
            rdatestart : pData[i].rdatestart,
            rdateend : pData[i].rdateend,
          })}
      }
      console.log(reservData);
      if(fiData.length===0){
      // setReservData(fiData);
        fiData.push(reservData);
        fiData=fiData[0];
      }

      console.log(fiData);
      if(fiData.length!==0&&paybtn===true){
      axios.post("/insertReservation" , fiData)
      .then((res) => {console.log(res);
          fiData=null;
          setReservData([]);
          setPayBtn(false);
          nav(0);
        }
      ).catch((err)=>{
        fiData=[];
        setReservData([]);
        setPayBtn(false);
      });
    }
    },[paybtn])
  
const onClickPayment = () => {
  console.log(data)
  if(id===undefined || id===null || id===""){
    window.alert("로그인 후 이용 가능한 서비스입니다.");
    return;
  }
  if(pData?.length===0){
    window.alert("찜목록을 선택해주세요!")
    return;
  }
  console.log(pData)
  for(let i = 0; i<pData?.length; i++){
    switch(pData[i].dtype){
      case "웨딩홀":
        if(pData[i].rdatestart===undefined){
          window.alert("웨딩홀 예약일을 선택해주세요!");
          return;
        }else if(pData[i].rperson===undefined){
          window.alert("인원을 입력해주세요!");
          return;
        };
        break;
      case "스드메" :
        if(pData[i].rdatestart===undefined){
          window.alert("스드메 예약일을 선택해주세요!");
          return;
        };
        break;
      case "플래너" :
        if(pData[i].rdatestart===undefined){
          window.alert("플래너 예약일을 선택해주세요!");
          return;
        };
        break;
      case "허니문" :
        if(pData[i].rdatestart===undefined){
          window.alert("출발날짜를 선택해주세요!");
          return;
        } else if(pData[i].rdateend===undefined){
          window.alert("종료날짜를 선택해주세요!");
          return;
        }
        break;
    }
  }

    // imp51345423
    console.log(data);
  const { IMP } = window;
  IMP.init("imp18221811"); // 결제 데이터 정의
  IMP.request_pay(data, callback);  //data에는 결제를 위한 정보들을 담은 객체를 전달해야 합니다. 예를 들어, buyer_name(주문자명), amoun(결제 금액), pg(사용할 PG사), pay_method(결제수단) 등이 존재합니다.
  console.log(data);
}                                   //callback 정보를 이용해 결제창을 호출하고, 유저가 입력한 카드 정보들이 카드사 서버로 전달되어 인증을 거치고, 인증이 성공하면 인증키를 PG에 전달하는 등 복잡한 과정을 거친 후, 콜백 함수가 호출됩니다


  const callback = (response) => {
    const {success, error_msg, imp_uid, merchant_uid, pay_method, paid_amount, status} = response;
    const tokenData={
      "imp_uid" : imp_uid
    }

    if (success) {
      console.log(imp_uid);
      if(wlist!==undefined){
        setReservData([...reservData,{
          rwhidx: wlist.whidx,
          rcost:paid_amount,
          rmid:id,
          rimpuid: imp_uid,
          rtype:"웨딩홀",
          rstatus : "진행예정",
        }])
      }else if(slist!==undefined){
        setReservData([...reservData,{
          rsidx: slist.sidx,
          rcost:paid_amount,
          rmid:id,
          rimpuid: imp_uid,
          rtype:"스드메",
          rstatus : "진행예정",
        }])
      }else if(plist!==undefined){
        setReservData([...reservData,{
          rpidx: plist.pidx,
          rcost:paid_amount,
          rmid:id,
          rimpuid: imp_uid,
          rtype:"플래너",
          rstatus : "진행예정",
        }])
      }else if(hlist!==undefined){
        setReservData([...reservData,{
          rhidx: hlist.hidx,
          rcost:paid_amount,
          rmid:id,
          rimpuid: imp_uid,
          rtype:"허니문",
          rstatus : "진행예정",
        }])
      }

      if(pData?.length!==0&&pData!==undefined){
        // for(let i=0; i<pData.length; i++){
          if(pData[0]?.dtype==="웨딩홀"){
              setReservData([...reservData,{
                rhidx: pData[0].dwhidx,
                rcost: pData[0].dprice,
                rmid:id,
                rimpuid: imp_uid,
                rtype:"웨딩홀",
                rstatus : "진행예정",
              }])}else if(pData[0]?.dtype==="스드메"){
              setReservData([...reservData,{
                rhidx: pData[0].dsidx,
                rcost:pData[0].dprice,
                rmid:id,
                rimpuid: imp_uid,
                rtype:"스드메",
                rstatus : "진행예정",
              }])}else if(pData[0]?.dtype==="플래너"){
              setReservData([...reservData,{
                rhidx: pData[0].dpidx,
                rcost:pData[0].dprice,
                rmid:id,
                rimpuid: imp_uid,
                rtype:"플래너",
                rstatus : "진행예정",
              }])}else if(pData[0]?.dtype==="허니문"){
              setReservData([...reservData,{
                rhidx: pData[0].dhidx,
                rcost:pData[0].dhprice,
                rmid:id,
                rimpuid: imp_uid,
                rtype:"허니문",
                rstatus : "진행예정",
              }])}
          // }
      }
      
      window.alert('결제 성공');
      setPayBtn(true);
    } else {
      window.alert(`결제 실패 : ${error_msg}`);
    }
  }
  
  return (
    <>
      <span onClick={onClickPayment}><Button style={{width:`${width}`, height:`${height}`, zIndex:`${zIndex}`, background:`${background}`, borderRadius:`${borderRadius}`}}>{ptext}</Button></span>
    </>
   );
}
  
  export default Payment;
```
'예약하기' 버튼을 클릭 하면 결제 모듈이 나타나고 실제 결제가 진행 됩니다. 해당 상품의 이름과 가격이 모듈에 나타나도록 설정 했습니다.

## Back_PaymentController
```java
@CrossOrigin(origins ="http://localhost:3000")
@RestController
@Log
public class PaymentController {
        //    @Value("${pgmodule.imp_uid}")
    @Value("${pgmodule.imp_key}")
    public String imp_key;
    @Value("${pgmodule.imp_secret}")
    public String imp_secret;

    @Autowired
    PaymentService pServ;
        @PostMapping("/insertReservation")
    public String insertReservation(@RequestBody List<Reservations> reservations){
        log.info("insertReservation()");
        log.info(""+reservations);
        String msg=pServ.insertReservation(reservations);
        return msg;
    }

    @GetMapping("/myReservation")
    public Map myReservation(@RequestParam String mid){
        log.info("myReservation()");
        log.info(mid);
        return pServ.myReservation(mid);
    }

    @PostMapping("/TokenRequest")
    public String TokenRequest(@RequestBody Map refundData){
        log.info("이게 뭐게???"+refundData.get("imp_uid"));
        log.info("이게 뭐게???"+imp_secret);
        log.info("이게 뭐게???"+imp_key);
        String imp_uid = refundData.get("imp_uid").toString();
        log.info(imp_uid);
        String access=pServ.TokenRequest(imp_key, imp_secret);
        log.info("토큰"+access);
//        pServ.getBuyerInfo(imp_uid, access);
        String res=refundCall(imp_uid, access);
        pServ.getBuyerInfo(imp_uid, access);

        return res;
    }
//    tokenRequest end

    @PostMapping("/refundCall")
    public String refundCall(String imp_uid, String access){
        log.info("이얻앙ㅁㅁㄴ엄ㄴ안ㅁ안언ㅁ엄ㄴㅇ"+access);
        String res = pServ.refundCall(imp_uid, access);
        return res;
    }

    @PostMapping("delReserv")
    public String delReserv(@RequestBody Map delReserv){
        log.info("delReserv()");
        log.info("das"+delReserv.toString());
        String ridx= delReserv.get("ridx").toString();
        log.info(""+ridx);
        String res=pServ.delReserv(Integer.parseInt(ridx));
        return res;
    }

}
```
## Back_PaymentService
```java
        @Service
@Log
public class PaymentService {
    @Autowired
    PaymentRepository pRepo;
    @Autowired
    ReservationRepository rRepo;
    @Autowired
    DibRepository dRepo;
    @Autowired
    WeddingHoleRepository wRepo;
    @Autowired
    SDMRepository sRepo;
    @Autowired
    PlannerRepository planRepo;
    @Autowired
    HoneyMoonRepository hRepo;

    @Transactional
    public String inputData(Refund refund){
        log.info("inputData()");
        String res = null;
        log.info(refund.getMerchant_uid());
        try {
            pRepo.save(refund);
            res = "Ok";
        }catch (Exception e){
            e.printStackTrace();
            res = "Fail";
        }
        log.info(res);
        return res;
    }

    @PostMapping("/getBuyerInfo")
    public void getBuyerInfo(String imp_uid, String access){
        RestTemplate restTemplate= new RestTemplate();
        log.info("이얻앙ㅁㅁㄴ엄ㄴ안ㅁ안언ㅁ엄ㄴㅇ"+access);
        HttpHeaders headers= new HttpHeaders();
    //        headers.add(HttpHeaders.ACCESS_CONTROL_ALLOW_ORIGIN, "https://api.iamport.kr/");
    //        headers.ACCESS_CONTROL_ALLOW_ORIGIN("sdfdd", headers.add();)
        headers.setContentType(MediaType.APPLICATION_JSON);
        headers.add("Authorization", "Bearer "+access);

        Map<String, Object> body=new HashMap<>();
        body.put("imp_uid", imp_uid);
    //        body.put("imp_key", imp_key);
    //        body.put("imp_secret", imp_secret);
        Gson var = new Gson();
        String json= var.toJson(body);
        //
        try{
            HttpEntity<String> entity=new HttpEntity<>(json, headers);
            log.info("이게 뭐게???"+entity);
            log.info("이게 뭐게???"+entity.getBody());
            log.info("이게 뭐게???"+entity.getHeaders());
            log.info("이게 뭐게???"+entity.getClass());
            log.info("이게 뭐게???"+ JSONObject.class);
            ResponseEntity<String> buyerInfo=restTemplate.postForEntity("https://api.iamport.kr/payments/"+imp_uid, entity, String.class);

            System.out.println(buyerInfo+"fullBuyerInfo");
            System.out.println(buyerInfo.getBody()+"fullbuyerInfo");
    //            System.out.println(token.getStatusCode()+"getToken");
    //            System.out.println(token.getStatusCodeValue()+"getTokenValue");
    //            System.out.println(token.getBody()+"tokenBody");
    //            System.out.println(token.getBody().get("response")+"tokenBody");
        }catch (Exception e){
           e.printStackTrace();
        }
    }

    public String insertReservation(List<Reservations> reservations) {
        String msg=null;
        log.info("이게 정보다아아"+reservations.toString());
        try {
            for(Reservations rList : reservations) {
                rRepo.save(rList);
                switch (rList.getRtype()){
                    case "웨딩홀":
                        dRepo.deleteByDwhidxmid(rList.getRwhidx(), rList.getRmid());
                        break;
                    case "스드메":
                        dRepo.deleteByDsidxmid(rList.getRsidx(), rList.getRmid());
                        break;
                    case "플래너":
                        dRepo.deleteByDpidxmid(rList.getRpidx(), rList.getRmid());
                        break;
                    case "허니문":
                        dRepo.deleteByDhidxmid(rList.getRhidx(), rList.getRmid());
                        break;
                }
            }
            msg="성공";
        }
        catch(Exception e){
            e.printStackTrace();
            msg="실패";
        }
        return msg;
    }


    public Map myReservation(String mid) {
        List<Reservations> rList = new ArrayList<>();
        List<WeddingHall> wList= new ArrayList<>();
        List<SDM> sList= new ArrayList<>();
        List<Planner> pList= new ArrayList<>();
        List<HoneyMoon> hList= new ArrayList<>();
        Map tMap = new HashMap();
        try{
            rList = rRepo.findByRmid(mid);
            for(Reservations rno : rList){
                switch (rno.getRtype()){
                    case "웨딩홀":
                        wList.add(wRepo.findByWhidx(rno.getRwhidx()));
                        break;
                    case "스드메":
                        sList.add(sRepo.findBySidx(rno.getRsidx()));
                        break;
                    case "플래너":
                        pList.add(planRepo.findByPidx(rno.getRpidx()));
                        break;
                    case "허니문":
                        hList.add(hRepo.findByHidx(rno.getRhidx()));
                        break;
                }
            }
        log.info("돌리기전"+pList);
            for(Reservations rno : rList){
                switch(rno.getRtype()){
                    case "웨딩홀":
                        for(WeddingHall wno : wList){
                            if(wno.getWhidx()==rno.getRwhidx()){
                                wno.setWhrList(rno);
                            }
                        }
                        break;
                    case "스드메":
                        for(SDM sno : sList){
                            if(sno.getSidx()==rno.getRsidx()){
                                sno.setSrList(rno);
                            }
                        }
                        break;
                    case "플래너":
                        for(Planner pno : pList){
                            if(pno.getPidx()==rno.getRpidx()){
                                pno.setPrList(rno);
                            }
                        }
                        break;
                    case "허니문":
                        for(HoneyMoon hno : hList){
                            if(hno.getHidx()==rno.getRhidx()){
                                hno.setHrList(rno);
                            }
                        }
                        break;
                }
            }
                log.info("돌린후"+pList);
            tMap.put("rw", wList);
            tMap.put("rs", sList);
            tMap.put("rp", pList);
            tMap.put("rh", hList);


        }catch(Exception e){
            e.printStackTrace();
        }

        return tMap;
    }

    public String TokenRequest(String imp_key, String imp_secret) {
        RestTemplate restTemplate = new RestTemplate();

        HttpHeaders headers = new HttpHeaders();
//        headers.add(HttpHeaders.ACCESS_CONTROL_ALLOW_ORIGIN, "https://api.iamport.kr/");
//        headers.ACCESS_CONTROL_ALLOW_ORIGIN("sdfdd", headers.add("access","*",));
        headers.setContentType(MediaType.APPLICATION_JSON);

        Map<String, Object> body = new HashMap<>();
//        body.put("imp_uid", imp_uid);
        body.put("imp_key", imp_key);
        body.put("imp_secret", imp_secret);
        Gson var = new Gson();
        String json = var.toJson(body);
        String access = null;
        try {
            HttpEntity<String> entity = new HttpEntity<>(json, headers);
            log.info("이게 뭐게???" + entity);
            log.info("이게 뭐게???" + entity.getBody());
            log.info("이게 뭐게???" + entity.getHeaders());
            log.info("이게 뭐게???" + entity.getClass());
            log.info("이게 뭐게???" + JSONObject.class);
            ResponseEntity<String> token = restTemplate.postForEntity("https://api.iamport.kr/users/getToken", entity, String.class);

            System.out.println(token + "fullToken");
            System.out.println(token.getBody() + "fullToken");
//            System.out.println(token.getStatusCode()+"getToken");
////            System.out.println(token.getStatusCodeValue()+"getTokenValue");
////            System.out.println(token.getBody()+"tokenBody");
//            System.out.println(token.getBody().get("response")+"tokenBody");
            access = token.getBody().substring(53, 93);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return access;
    }


    public String refundCall(String imp_uid, String access) {
        RestTemplate restTemplate= new RestTemplate();
        String res = "Failed";
        HttpHeaders headers= new HttpHeaders();
//        headers.add(HttpHeaders.ACCESS_CONTROL_ALLOW_ORIGIN, "https://api.iamport.kr/");
//        headers.ACCESS_CONTROL_ALLOW_ORIGIN("sdfdd", headers.add();)
        headers.setContentType(MediaType.APPLICATION_JSON);
        headers.add("Authorization", "Bearer "+access);

        Map<String, Object> body=new HashMap<>();
        body.put("imp_uid", imp_uid);
//        body.put("imp_key", imp_key);
//        body.put("imp_secret", imp_secret);
        Gson var = new Gson();
        String json= var.toJson(body);
        try{
            HttpEntity<String> entity=new HttpEntity<>(json, headers);
            log.info("이게 뭐게???"+entity);
            log.info("이게 뭐게???"+entity.getBody());
            log.info("이게 뭐게???"+entity.getHeaders());
            log.info("이게 뭐게???"+entity.getClass());
            log.info("이게 뭐게???"+JSONObject.class);
            ResponseEntity<String> buyerInfo=restTemplate.postForEntity("https://api.iamport.kr/payments/cancel", entity, String.class);

            System.out.println("환불 성공");
            System.out.println(buyerInfo+"fullBuyerInfo");
            System.out.println(buyerInfo.getBody()+"fullbuyerInfo");
//            System.out.println(token.getStatusCode()+"getToken");
//            System.out.println(token.getStatusCodeValue()+"getTokenValue");
//            System.out.println(token.getBody()+"tokenBody");
//            System.out.println(token.getBody().get("response")+"tokenBody");
            res="Success";
        }catch (Exception e){
            e.printStackTrace();
        }
        return res;
    }

    public String delReserv(int ridx) {
        String res="Failed";
        Reservations rData = new Reservations();
        try{
            rData=rRepo.findByRidx(ridx);
            rData.setRstatus("환불완료");
            rRepo.save(rData);
            res="Success";
        }catch (Exception e){
            e.printStackTrace();
        }
        return res;
    }

}
```
프론트에서 보낸 값으로 결제가 성공했다면 데이터베이스에 해당 결제 상품을 저장해 줍니다.<br><br>
- #### 예약 버튼 클릭 후 화면<br><br>
<img width="1105" alt="단일결제화면" src="https://user-images.githubusercontent.com/117880554/224941702-14e23193-f0d2-415d-9e01-f05f107c9cbc.png">
<br><br>

## 2. 이벤트 팝업창

※ EventModal.jsx
```javascript

const Container = styled.div`
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
`;

const ModalBackground = styled.div`
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.2);
  z-index: 1000;
`;

const ModalContainer = styled.div`
  z-index: 1001;
`;

const ModalContent = styled.div`
  width: 30vw;
  height: 35vw;
  margin: 0 100%;
  margin-bottom: 10px;
  border-radius: 10px;
  background-image: url(${(props)=>(props.eData ? "upload/"+props.eData : "upload/"+props.eData)});
  background-size: 30vw 35vw;
  background-repeat: no-repeat;
  background-position: center center;
`;

const ModalCloseWrapper = styled.div`
    width:100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 100%;
  p, label {
    cursor: pointer;
    color: white;
  },
  input {
    margin-right:5px
  }
`;

const EventModal = ({closeModal, closeModalUntilExpires, eData}) => {
  console.log(eData[0]);
  return (
    <Container>
      <ModalBackground />
      <ModalContainer>
        <ModalContent eData={eData[0]?.eimg}>
        </ModalContent>
        <ModalCloseWrapper>
          <label><input type={"checkBox"} onClick={closeModalUntilExpires}/>오늘 하루 더 이상 보지 않기</label>
          <p onClick={closeModal}>닫기 x</p>
        </ModalCloseWrapper>
      </ModalContainer>
    </Container>
  );
}

export default EventModal;
```
※ EventModalControll.jsx
```javascript

export default () => {
  const [eData, setEdata]= useState([]);
  useEffect(()=>{
    axios.get("/eventGet").then((res)=>{console.log(res); setEdata(res.data)}).catch(err=>console.log(err));
  },[])
  console.log(eData);
  const [openModal, setOpenModal] = useState(true);
  const [hasCookie, setHasCookie] = useState(true);
  const [appCookies, setAppCookies] = useCookies(); 

  const getExpiredDate = (days) => {
    const date = new Date();
    date.setDate(date.getDate() + days);
    return date;
  };

  const closeModalUntilExpires = () => {
    if (!appCookies) return;

    const expires = getExpiredDate(1);
    setAppCookies("MODAL_EXPIRES", true, { path: "/", expires });

    setOpenModal(false);
  };

  useEffect(() => {
    if (appCookies["MODAL_EXPIRES"]) return;
    console.log(appCookies["MODAL_EXPIRES"]);
    setHasCookie(false);
  }, []);
  

  return (
    <div>
      {openModal && !hasCookie && <EventModal closeModal={() => setOpenModal(false)} closeModalUntilExpires={closeModalUntilExpires} eData={eData} />}
    </div>
  );
}
```

- #### 메인 페이지 화면<br>
<img width="1106" alt="팝업창" src="https://user-images.githubusercontent.com/117880554/224937495-2a248b86-fe4c-4efc-8c37-d640e9fe6513.png">

- #### 오늘 하루 보지 않기 클릭 후 쿠키 기록<br>
<img width="785" alt="쿠키" src="https://user-images.githubusercontent.com/117880554/224944468-6c31f862-02b0-403c-9862-addfc26847cf.png">

페이지에 들어가자마자 팝업창을 띄워줍니다. '오늘 하루 보지 않기' 버튼을 클릭했을때 쿠키를 사용해서 더 이상 팝업창이 뜨지 않도록 설정해주었습니다.

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

## Likes.jsx(마이페이지 찜목록) 

```javascript
    export default () => {
      const comma = (num) =>[num].toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
      const id = sessionStorage.getItem("mid");
      const nav = useNavigate();
        const inputBorder= useRef();
      const [dibData,setDibData] = useState([{}]);
      useEffect(()=>{
        axios.post("/searchDib", null, {params:{mid:id}})
        .then((res)=>{
          console.log(res.data);
          setDibData(res.data);
        })
      },[])

      const [likes, setLikes] = useState([
        // {name: "gd"},
        // {name: "gd"},
        // {name: "gd"},
      ])
      console.log(dibData);
      const {wh,sd,pl,ho} = dibData;
      useEffect(()=>{
        console.log(wh);
        let ls = [];
        if(wh!==undefined){
          for(let i=0; i<wh.length; i++){
            ls.push({dname: wh[i].whname, dtype: "웨딩홀", dprice: wh[i].whprice ,dwhidx:wh[i].whidx, dmid:id, bprice: wh[i].bprice ,dorder: i});
            setLikes(ls);
          }
        }
          if(sd!==undefined){
            for(let i=0; i<sd.length; i++){
              ls.push({dname: sd[i].scomp, dtype: "스드메", dprice: sd[i].sprice ,dsidx:sd[i].sidx, dmid:id, dorder: wh.length+i,});
              setLikes(ls);
            }
          }
          if(pl!==undefined){
            for(let i=0; i<pl.length; i++){
              ls.push({dname: pl[i].pname, dtype: "플래너", dprice: pl[i].pprice ,dpidx:pl[i].pidx, dmid:id, dorder: wh.length+sd.length+i,});
              setLikes(ls);
            }
          }
          if(ho!==undefined){
            for(let i=0; i<ho.length; i++){
              ls.push({dname: ho[i].hlocation, dtype: "허니문", dprice: ho[i].hcost ,dhidx:ho[i].hidx, dmid:id, dorder: wh.length+sd.length+pl.length+i,});
              setLikes(ls);
            }
          }
      },[wh],[sd],[pl],[ho]);
      // console.log({a})
      // likes.concat();
      // for(let i=1; i<3; i++){
      //   likes.concat({name: dd[i]});
      // }
      // console.log(likes)
      const [delData, setdelData] = useState([]);
      const [delbtn, setDelbtn] = useState(false);

      // const onRemoveHandler = (id) => () => {
      //   if (!window.confirm(`${likes[id].name} 을 찜 목록에서 삭제하시겠습니까?`)) return


      // }
      const [showData,setShowData]=useState([]);;
      useEffect(()=>{
        let tempShow = []
        console.log(likes);
        tempShow=likes.slice();
        console.log(tempShow)
          for(let i =0; i<tempShow.length; i++){
            tempShow[i]={...tempShow[i], dprice:comma(tempShow[i].dprice)}
        }
        setShowData(tempShow);
        console.log(showData);
      },[likes])


      useEffect(()=>{
        console.log("여기요오오"+delData);
        if(delbtn===true){
          axios.post("/deleteDib", delData)
          .then((res)=>{
            window.alert("힝 삭제됐어");
            setDelbtn(false);
            nav(0);
          });  
        }


        //버튼누를때 유즈스테이트 하나 바뀌게해서 만약에 그값이 바뀌면 axios 보낸다 해주면될듯
      },[delData,delbtn]);

      const [checkall,setCheckall] = useState(false);
      const [checkList, setCheckList] = useState([]);
      // useEffect(()=>{
      //   console.log(delData,checkall);
      // },[delData,checkall])
      let tempdelData = [];
      let tempcheckList = [];
      let tempallData= [];
      const onCheckboxChangeHandler = (e,index) => {
        console.log(checkList.length, likes.length);
        console.log(index);
        if (e.target.name!=="rperson" && e.target.name!=="rdatestart" && e.target.name!=="rdateend"){
          const val = Number(e.target.value)
          setCheckList(checkList.includes(val) ? checkList.filter((v) => v !== val) : [...checkList, val])
          console.log(val);
          console.log(checkList);
          {val ===-1&&checkall===false ? setCheckall(true): setCheckall(false)};
          if(val===-1&&delData.length!==likes.length){
            setCheckList([]);
            setdelData([]);
            setdelData(likes);
            console.log("제바아아알")
            console.log(delData);
            return;
          }else if(val===-1){
            // setCheckList(checkList.filter(v=> v !== val));
            setCheckall(false);
            setdelData([]);
            console.log(delData);
            return;
          }else if (val!==-1&&delData.length===likes.length){
            setCheckall(false);
            console.log(delData);
            console.log(checkList);
            for(let i = 0 ; i<likes.length; i++){
              tempcheckList.push(i);
            }
            tempcheckList.splice(val,1);
            setCheckList(tempcheckList);
            tempallData = delData.slice();
            tempallData.splice(val,1);
            setdelData(tempallData);
            return;
          }




          console.log(e.target.checked,checkall)
          console.log(likes[e.target.value].dtype, e.target.checked, checkall)
          if(likes[e.target.value].dtype==="웨딩홀"&&e.target.checked===true &&checkall===false){
            setdelData([...delData,{
              dtype:"웨딩홀",
              dmid:id,
              dwhidx:likes[e.target.value].dwhidx,
              dprice:likes[e.target.value].dprice,
              dname:likes[e.target.value].dname,
              dorder: index,
              bprice: likes[e.target.value].bprice
          }])}else if(likes[e.target.value].dtype==="웨딩홀"&&e.target.checked===false &&checkall===false){
            setdelData(delData.filter(delData=>delData.dwhidx!==likes[e.target.value].dwhidx))
          }
          if(likes[e.target.value].dtype==="스드메"&&e.target.checked===true &&checkall===false){
            console.log(likes[e.target.value].dsidx);
            setdelData([...delData,{
              dtype:"스드메",
              dmid:id,
              dsidx:likes[e.target.value].dsidx,
              dprice:likes[e.target.value].dprice,
              dname:likes[e.target.value].dname,
              dorder:index,
          }])}else if(likes[e.target.value].dtype==="스드메"&&e.target.checked===false &&checkall===false){
            setdelData(delData.filter(delData=>delData.dsidx!==likes[e.target.value].dsidx))
          }
          if(likes[e.target.value].dtype==="플래너"&&e.target.checked===true &&checkall===false){
            console.log(likes[e.target.value].dpidx);
            setdelData([...delData,{
            dtype:"플래너",
            dmid:id,
            dpidx:likes[e.target.value].dpidx,
            dprice:likes[e.target.value].dprice,
            dname:likes[e.target.value].dname,
            dorder:index,
          }])}else if(likes[e.target.value].dtype==="플래너"&&e.target.checked===false &&checkall===false){
            setdelData(delData.filter(delData=>delData.dpidx!==likes[e.target.value].dpidx))
          }
          if(likes[e.target.value].dtype==="허니문"&&e.target.checked===true &&checkall===false){
            console.log(likes[e.target.value].dhidx);
            setdelData([...delData,{
            dtype:"허니문",
            dmid:id,
            dhidx:likes[e.target.value].dhidx,
            dprice:likes[e.target.value].dprice,
            dname:likes[e.target.value].dname,
            dorder:index,
          }])}else if(likes[e.target.value].dtype==="허니문"&&e.target.checked===false &&checkall===false){
            setdelData(delData.filter(delData=>delData.dhidx!==likes[e.target.value].dhidx))
          }
        }


        if (e.target.name==="rperson" || e.target.name==="rdatestart" || e.target.name==="rdateend"){
          tempdelData=delData.slice();
          // console.log(delData.findIndex(d=>d.dorder===index));
          if(tempdelData.length!==0 &&e.target.name==="rperson"){
          tempdelData[delData.findIndex(d=>d.dorder===index)]={...tempdelData[delData.findIndex(d=>d.dorder===index)],[e.target.name]:parseInt(e.target.value)};
          setdelData(tempdelData);
          } else if(tempdelData.length!==0 &&e.target.name!=="rperson"){
            tempdelData[delData.findIndex(d=>d.dorder===index)]={...tempdelData[delData.findIndex(d=>d.dorder===index)],[e.target.name]:e.target.value};
            setdelData(tempdelData);
            }
          console.log(tempdelData);
          console.log(index);
          console.log(checkall)
        }
      }

      const borderChange = (e)=> {
        inputBorder.current.style.border="1px solid lightGray";
        inputBorder.current = e.target;
        inputBorder.current.style.border="1px solid black";
      }
      const personRegExp = /^[0-9]{0,4}$/;
      const dataConfirm= (e) =>{
        if(!personRegExp.test(inputBorder.current.value)){
          window.alert("0명 이상 입력해주세요");
          inputBorder.current.value="";
        }
      }
      console.log(delData);
      return (
        <div style={{ width: '100%' }}>
          <Table
            columns={[
              {
                name: checkall === false ? <input type="checkBox" checked={false} value={-1} onChange={(e)=>onCheckboxChangeHandler(e)}/>:<input type="checkBox" checked={true} value={-1} onChange={(e)=>onCheckboxChangeHandler(e)}/>,
                render: (v, index) => (
                  checkall === true ? <input type="checkbox" value={index} onChange={(e)=>onCheckboxChangeHandler(e,index)} checked/> : checkall === false && checkList.indexOf(index) !== -1 ? <input type="checkbox" value={index} onChange={(e)=>onCheckboxChangeHandler(e,index)} checked/>:<input type="checkbox" value={index} onChange={(e)=>onCheckboxChangeHandler(e,index)}/>
                ),
              },
              {
                name: '등록번호',
                render: (v, index) => index + 1,
                style: {
                  width: 80,
                },
              },
              {
                name: '타입',
                id: 'dtype',
              },
              {
                name: '상품명',
                id: 'dname',
              },
              {
                name: '예약일 선택',
                render: (v,index) => ( checkall===false ?( likes[index].dtype !== "허니문" && checkList.indexOf(index) === -1 ? <input type="date" name="rdatestart" onChange={(e)=>onCheckboxChangeHandler(e, index)} style={{width:"300px", fontSize:"16px", textAlign:"center", border:"none"}} disabled/> : likes[index].dtype !== "허니문" && checkList.indexOf(index) !== -1 ? <input type="date" name="rdatestart" onChange={(e)=>onCheckboxChangeHandler(e, index)} style={{width:"300px", fontSize:"16px", textAlign:"center", border:"none"}}/> : checkList.indexOf(index) === -1 ? <><input type="date" disabled onChange={(e)=>onCheckboxChangeHandler(e,index)} name="rdatestart" style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/><span> ~ </span><input type="date" name='rdateend' disabled onChange={(e)=>onCheckboxChangeHandler(e,index)} style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/></> :  <><input type="date" onChange={(e)=>onCheckboxChangeHandler(e,index)} name="rdatestart" style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/><span> ~ </span><input type="date" name='rdateend' onChange={(e)=>onCheckboxChangeHandler(e,index)} style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/></>)
                :( likes[index].dtype !== "허니문" ? <input type="date" name="rdatestart" onChange={(e)=>onCheckboxChangeHandler(e, index)} style={{width:"300px", fontSize:"16px", textAlign:"center", border:"none"}}/> : <><input type="date" onChange={(e)=>onCheckboxChangeHandler(e,index)} name="rdatestart" style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/><span> ~ </span><input type="date" name='rdateend' onChange={(e)=>onCheckboxChangeHandler(e,index)} style={{width:"150px",fontSize:"16px", textAlign:"center", border:"none"}}/></>)),
                id: 'selectRdate',
              },
              {
                name: '1인 식대',
                render: (v,index) => likes[index].dtype === "웨딩홀"?<div type="text" name="bprice" style={{width:"50px", textAlign:"center"}}>{likes[index].bprice} 만원</div>: null,
                id: 'bprice',
              },
              {
                name: '인원 선택',
                render: (v,index) => ( checkall===false ?( likes[index].dtype === "웨딩홀" && checkList.indexOf(index) === -1 ?<><input type="text" disabled ref={inputBorder} onClick={(e)=>borderChange(e)} onChange={(e)=>{onCheckboxChangeHandler(e,index);dataConfirm(e)}} name="rperson" maxLength="4" style={{width:"50px", border:"1px solid lightGray", textAlign:"center"}}/><label style={{color:"black", marginLeft:"10px"}}>명</label></> : likes[index].dtype === "웨딩홀" && checkList.indexOf(index) !== -1 ?  <><input type="text" ref={inputBorder} onClick={(e)=>borderChange(e)} onChange={(e)=>{onCheckboxChangeHandler(e,index);dataConfirm(e)}} name="rperson" maxLength="4" style={{width:"50px", border:"1px solid lightGray", textAlign:"center"}}/><label style={{color:"black", marginLeft:"10px"}}>명</label></>:null)
                : ( likes[index].dtype === "웨딩홀" ?  <><input type="text" ref={inputBorder} onClick={(e)=>borderChange(e)} onChange={(e)=>{onCheckboxChangeHandler(e,index);dataConfirm(e)}} name="rperson" maxLength="4" style={{width:"50px", border:"1px solid lightGray", textAlign:"center"}}/><label style={{color:"black", marginLeft:"10px"}}>명</label></>:null)),
                id: 'selectPopu',
              },
              {
                name: '가격',
                render: (v,index) => likes[index].dtype === "웨딩홀" && (delData[delData.findIndex(d=>d.dorder===index)]?.rperson ===null || delData[delData.findIndex(d=>d.dorder===index)]?.rperson === undefined || delData[delData.findIndex(d=>d.dorder===index)]?.rperson === "")?<div type="text" name="dprice" style={{width:"100px", textAlign:"right"}}>{likes[index]?.dprice} 만원</div>: likes[index].dtype === "웨딩홀"&&(checkList.indexOf(index) !==-1||checkall)&&(delData[delData.findIndex(d=>d.dorder===index)]?.rperson !==null || delData[delData.findIndex(d=>d.dorder===index)]?.rperson !==undefined || delData[delData.findIndex(d=>d.dorder===index)]?.rperson !== "") ?<div type="text" name="dprice" style={{width:"100px", textAlign:"right"}}>{likes[index].dprice+delData[delData.findIndex(d=>d.dorder===index)].bprice*delData[delData.findIndex(d=>d.dorder===index)].rperson} 만원</div> : <div type="text" name="dprice" style={{width:"100px", textAlign:"right"}}>{likes[index].dprice} 만원</div>,
                id: 'dprice',
              },
            ]}
            dataSource={showData}
          />
          <div style={{float:"right", marginTop:'50px', width:200, display:"flex", justifyContent:"space-around"}}>
            <Button onClick={()=>setDelbtn(true)}>선택삭제</Button>
          <Payment ptext="결제하기" pData={delData} />
          </div>
        </div>
      )
    }
```
체크박스를 사용하여 체크된 상품들만 input태그의 disabled를 풀어주고 해당 상품에 필요한 옵션을 작성할 수 있고, 작성하지 않고 '결제하기' 버튼을 클릭 시 작성해달라는 경고창이 나타납니다. 체크한 상품들의 가격이 우측에 나오고, 옵션 작성으로 인한 가격 변동은 실시간으로 반영됩니다. 여러 상품을 선택하고 '결제하기'버튼을 클릭 시 결제 모듈이 나타나며 첫번째 상품의 이름과 함께 'xxx외 x건'으로 몇 건의 상품을 결제하는지가 모듈에 상품명으로 등록되어있고, 가격은 총 합산 가격으로 결제가 진행됩니다. 백은 결제에서 사용한 함수를 그대로 사용하였습니다.

#### 찜목록 화면<br><br>
<img width="1106" alt="찜목록" src="https://user-images.githubusercontent.com/117880554/224946446-3ba0d44d-01af-4e5d-a1f3-752989a22188.png">

#### 결제 모듈<br><br>
<img width="409" alt="합산 결제" src="https://user-images.githubusercontent.com/117880554/224946697-bf39d550-00c0-4734-9c0c-6b6a10c6e4e9.png">

## Reservation.jsx(마이페이지 예약 확인)
```javascript
    export default () => {
      const id = sessionStorage.getItem("mid");
      const nav = useNavigate();
      const [reservData, setReservData] = useState([]);
      const [reserv, setReserv]= useState([]);
      const [refundData, setRefundData]=useState({});
      const [delReserv, setDelReserv]=useState();
      const [a, setA]= useState(false);
      let total =[];
      let rList=[];
      let temprlist =[];
      useEffect(()=>{
        axios.get("/myReservation",{params:{mid : id}})
        .then((res)=>{
          console.log(res.data);
          setReservData(res.data);
        }).catch((error)=>console.log(error));
      },[])

      const {rw,rs,rp,rh} = reservData;
      rList.push(rw);
      rList.push(rs);
      rList.push(rp);
      rList.push(rh);
      console.log(rList);
      const inputReserv = rList;
      console.log(inputReserv);
      if(reservData.length!==0){
      if(rw.length!==0){
        for(let i=0; i<rw.length; i++){
          temprlist.push(rw[i].whrList);
        }
      }
      if(rs.length!==0){
        for(let i=0; i<rs.length; i++){
          temprlist.push(rs[i].srList);
        }
      }
      if(rp.length!==0){
        for(let i=0; i<rp.length; i++){
          temprlist.push(rp[i].prList);
        }
      }
      if(rh.length!==0){
        for(let i=0; i<rh.length; i++){
          temprlist.push(rh[i].hrList);
        }
      }
      const trList = temprlist;
      console.log(trList)
      for(let i=0; i<trList.length; i++){
        console.log(trList[i])
        console.log(inputReserv)
        switch(trList[i].rtype){
          case "웨딩홀":
            total.push({category :trList[i].rtype, name:inputReserv[0][i].whname, date:moment(trList[i].rdatestart).format('YYYY-MM-DD'), price:trList[i].rcost +" 만원", progress:trList[i].rstatus})
            break;
          case "스드메":
            total.push({category :trList[i].rtype, name:inputReserv[1][i-rw.length].scomp, date:moment(trList[i].rdatestart).format('YYYY-MM-DD'), price:trList[i].rcost+" 만원", progress:trList[i].rstatus})
            break;
          case "플래너":
            total.push({category :trList[i].rtype, name:inputReserv[2][i-rw.length-rs.length].pname, date:moment(trList[i].rdatestart).format('YYYY-MM-DD'), price:trList[i].rcost+" 만원", progress:trList[i].rstatus})
            break;
          case "허니문":
            total.push({category :trList[i].rtype, name:inputReserv[3][i-rw.length-rs.length-rp.length].hlocation, date:(moment(trList[i].rdatestart).format('YYYY-MM-DD') +" ~ " + moment(trList[i].rdateend).format('YYYY-MM-DD')), price:trList[i].rcost+" 만원", progress:trList[i].rstatus})
            break;
          }
          console.log(total);
      }
      console.log(total);
    }
      useEffect(()=>{
        setReserv(total);
      },[reservData])

      const onRemoveHandler = (index) => () => {
        if(temprlist[index].rstatus==="환불완료"){
          alert("이미 환불된 건입니다.");
          return;
        }
        let rconf=window.confirm("예약을 취소하시겠습니까?");
        console.log("여기보세요");
        console.log(temprlist[index].ridx);
        console.log(temprlist[index].rimpuid);
        console.log(temprlist[index].rcost);
        console.log(temprlist[index].rstatus);
        console.log(reserv[index].name);
        if(rconf===true){
        setRefundData({
          imp_uid:temprlist[index].rimpuid,
          cancel_request_amount:temprlist[index].rcost,
          reason: "테스트 결제 환불", // 환불사유
        });
        setDelReserv({ridx:temprlist[index].ridx});
      }
        console.log(refundData);

      }
      console.log(refundData);
        useEffect(()=>{
          if(refundData.length===0){
            return;
          }
          axios.post("/TokenRequest", refundData)  //환불전에 토큰받고 환불로이어짐
          .then((res)=>{
              console.log(res.data);
              setRefundData([]);
              setA(true);
          }).catch((err)=>{console.log(err);setRefundData([]);})
        },[refundData]);

        useEffect(()=>{
          console.log(delReserv);
          if(a===true){
            axios.post("/delReserv",delReserv)
            .then((res)=>{
              console.log("예약삭제?",res.data);
              setA(false);
              window.alert("예약이 취소되었습니다");
              nav(0);
            }).catch((err)=>{
              console.log(err);
              setA(false);
            })
          }
        },[a]);

      return (
        <Table
          columns={[
            {
              name: '예약 번호',
              render: (v, index) => index + 1,
              style: {
                width: 80,
              },
            },
            {
              name: '예약 종류',
              id: 'category',
            },
            {
              name: '예약 명',
              id: 'name',
            },
            {
              name: '예약 날짜',
              id: 'date',
            },
            {
              name: '예약금',
              id: 'price',
            },
            {
              name: '진행 현황',
              id: 'progress',
            },
            {
              name: '확인/취소',
              id: 'id',
              render: (v, index) => (temprlist[index].rstatus === "진행예정" ? <Button onClick={onRemoveHandler(index)}>예약취소</Button>:<Button onClick={onRemoveHandler(index)} style={{background:"red"}}>환불완료</Button> ),
              style: {
                width: 200,
              },
            },
          ]}
          dataSource={reserv}
        />
      )
    }
```
결제가 완료된 상품들이 정렬되어 나타나고 해당 상품들의 정보와 진행상황이 나타납니다. '환불하기' 버튼 클릭 시 확인 경고창이 나타나고 환불 진행 시 실제로 환불처리가 되며 진행상황이 '환불완료'로 바뀌게 됩니다. 환불완료된 상품의 '환불하기' 버튼 클릭 시 이미 환불된 건이라는 알림창이 나타납니다. 백은 결제에서 사용한 함수를 그대로 사용하였습니다.

#### 예약확인 화면<br><br>
<img width="858" alt="예약확인" src="https://user-images.githubusercontent.com/117880554/224947323-f9e978bd-9b1d-4b57-bd67-e6a0a1005af3.png">


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
프로젝트를 시작하기 전 리액트를 3~4일 정도만 배웠어서 코드 자체가 번잡한 부분이 많은것 같습니다. 더 열심히 해서 점점 나아지는 모습 기대해주세요. 이 프로젝트는 저에게는 많은 경험이 되었고, 저의 부족한 부분과 제가 할 수 있는 부분을 구별할 수 있는 능력을 가지게 해주었다고 생각합니다. 그렇기에 부족한 부분은 더 공부하고, 할 수 있는 부분은 까먹지 않게 노력해야 될것 같습니다.
